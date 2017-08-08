title: Redis实现分布式锁
author: Cary
date: 2017-08-08 17:30:42
tags:
---
## Redis实现分布式锁
#### 分布式锁的一些问题
1. 并发问题，若多个客户端同时上锁，结果只允许一个客户端成功，其他失败，可以利用redis的`SETNX` 命令来实现，该命令允许若给定的 key 已经存在，则 `SETNX` 不做任何动作,设置成功，返回 1 ,设置失败，返回 0 。
1. 上锁后解锁的问题，可以考虑使用redis key的ttl过期，通过`PEXPIRE`来设置key的自动过期。若不使用自动过期特性，则需要在锁定结束后使用`DEL`命令来进行解锁，这种情况有可能发生某个客户端已经crash，于是这个锁会永远锁定，导致其他客户端无法获得锁。

#### Redis2.6以后新特性
redis2.6.12以后 SET 命令的行为可以通过一系列参数来修改
1. EX second ：设置键的过期时间为 second 秒。 `SET key value EX second` 效果等同于 `SETEX key second value` 。
1. PX millisecond ：设置键的过期时间为 millisecond 毫秒。 `SET key value PX millisecond` 效果等同于 `PSETEX key millisecond value` 。
1. NX ：只在键不存在时，才对键进行设置操作。 `SET key value NX` 效果等同于 `SETNX key value` 。
1. XX ：只在键已经存在时，才对键进行设置操作。

#### 使用新特性来解决分布式锁
1. 使用命令 `SET key value NX EX second` 设置锁的同时为锁设置TTL过期时间，若当锁已经存在时返回nil。

#### Redisson解决方法
[Redisson](https://github.com/redisson/redisson/wiki/Redisson%E9%A1%B9%E7%9B%AE%E4%BB%8B%E7%BB%8D)是redis的一个java客户端,实现了分布式锁和同步器，Redisson的分布式锁RLock Java对象实现了java.util.concurrent.locks.Lock接口，同时还支持自动过期解锁。
```
RLock lock = redisson.getLock("anyLock");
// 最常见的使用方法
lock.lock();

// 支持过期解锁功能
// 10秒钟以后自动解锁
// 无需调用unlock方法手动解锁
lock.lock(10, TimeUnit.SECONDS);

// 尝试加锁，最多等待100秒，上锁以后10秒自动解锁
boolean res = lock.tryLock(100, 10, TimeUnit.SECONDS);
...
lock.unlock();

```

以上是redisson使用锁的方法，它的原理采用了lua脚本的方式，这样能兼容redis 2.6.12之前的版本,锁的核心源码如下RedissonLock.java
```
<T> RFuture<T> tryLockInnerAsync(long leaseTime, TimeUnit unit, long threadId, RedisStrictCommand<T> command) {
        internalLockLeaseTime = unit.toMillis(leaseTime);

        return commandExecutor.evalWriteAsync(getName(), LongCodec.INSTANCE, command,
        //先检查key是否存在
                  "if (redis.call('exists', KEYS[1]) == 0) then " +
        //key不存在，创建Hash
                      "redis.call('hset', KEYS[1], ARGV[2], 1); " +
        //设置过期时间
                      "redis.call('pexpire', KEYS[1], ARGV[1]); " +
                      "return nil; " +
                  "end; " +
        //若锁已经存在，并且是同样获得锁的线程调用
                  "if (redis.call('hexists', KEYS[1], ARGV[2]) == 1) then " +
        //复用锁，为锁+1
                      "redis.call('hincrby', KEYS[1], ARGV[2], 1); " +
        //延长锁定时间
                      "redis.call('pexpire', KEYS[1], ARGV[1]); " +
                      "return nil; " +
                  "end; " +
         //若无法获得锁，返回锁的剩余时间
                  "return redis.call('pttl', KEYS[1]);",
                    Collections.<Object>singletonList(getName()), internalLockLeaseTime, getLockName(threadId));
    }
    
```