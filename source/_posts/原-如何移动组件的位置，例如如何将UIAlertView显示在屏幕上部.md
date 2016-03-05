---
title: '[原]如何移动组件的位置，例如如何将UIAlertView显示在屏幕上部'
tags: []
date: 2010-05-26 16:59:00
---

苹果自带的警告框非常好用，但是它总是显示在屏幕中间，我们如何将它的位置移动呢？从Iphone SDK3开始我们可以使用CGAffineTransformTranslate

<!-- more -->

<textarea cols="50" rows="15" name="code" class="c-sharp">UIAlertView * alert = [ [ UIAlertView alloc ] initWithTitle:@"Alert" message:@"Alert" 
                        delegate:self cancelButtonTitle:@"OK" otherButtonTitles:nil ];
alert.transform = CGAffineTransformTranslate( alert.transform, 0.0, 100.0 );
[ alert show ];</textarea>&nbsp;`CGAffineTransformTranslate`&nbsp;有3个参数: 组件的 transform, x transform,y transform. 在代码中, 我将alert上移动了100个宽度。

&nbsp;

            <div>
                作者：wherejaly 发表于2010/5/26 16:59:00 [原文链接](http://blog.csdn.net/wherejaly/article/details/5625903)
            </div>
            <div>
            阅读：2207 评论：0 [查看评论](http://blog.csdn.net/wherejaly/article/details/5625903#comments)
            </div>