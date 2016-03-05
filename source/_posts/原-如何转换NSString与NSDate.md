---
title: '[原]如何转换NSString与NSDate?'
tags: []
date: 2010-04-30 11:47:00
---

&nbsp;&nbsp; &nbsp; 想要在NSString与NSDate之间进行转换，答案是使用NSDateFormatter,该类提供了&ndash; dateFromString: 和&ndash; stringFromDate:两个关键的方法，具体使用请看如下代码：

<textarea cols="50" rows="15" name="code" class="cpp">NSDateFormatter *formatter = [[NSDateFormatter alloc] init];
[formatter setDateFormat:@"yyyy"];
//Optionally for time zone converstions
[formatter setTimeZone:[NSTimeZone timeZoneWithName:@"..."]];
NSString *stringFromDate = [formatter stringFromDate:myNSDateInstance];</textarea>&nbsp;

参考资料：http://stackoverflow.com/questions/576265/convert-nsdate-to-nsstring

            <div>
                作者：wherejaly 发表于2010/4/30 11:47:00 [原文链接](http://blog.csdn.net/wherejaly/article/details/5545712)
            </div>
            <div>
            阅读：2799 评论：0 [查看评论](http://blog.csdn.net/wherejaly/article/details/5545712#comments)
            </div>