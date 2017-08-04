title: "could not read Username for 'https://github.com': Invalid argument"
author: Cary
date: 2017-08-04 12:23:47
tags:
---
## could not read Username for 'https://github.com': Invalid argument

好久没玩hexo blog了，今天心血来潮想恢复使用，结果发现使用`hexo d`命令时会报如下错误

```
could not read Username for 'https://github.com': Invalid argument


```



网上搜索了下，这个问题有以下几个原因：

1. 如果安装git客户端的时候没有勾选git命令在bash和cmd命令都有效，若是在cmd命令下则因为没有将git添加到windows的path，所以会出现这个错误，一般可以尝试在blog的目录打开git bash再尝试`hexo d`。

2. 未将username和email加入到git，可以使用如下命令试试

```
git config --global user.name "yourname"
git config --global user.email "youremail"

```

3. 检查`_config.yml`的配置是否正确

```
 deploy:
  type: git
  repo: https://github.com/yourname/yourname.github.io.git
  branch: master
```

4. 客户端太老，我遇到就是这个问题，即便切换了git bash也仍然报错，于是我升级了新客户端，结果能正常弹出github的用户名和密码输入框，确认后可以正常部署。