---
title: '[原]如何在navigationBar的中间添加一张自定义图片？'
tags: []
date: 2010-05-12 14:51:00
---

以下代码展示了如何在navigationBar中间添加一张自定义图片

<textarea cols="50" rows="15" name="code" class="c-sharp">UIImage *image = [UIImage imageNamed: @"NavBarImage.png"];
UIImageView *imageView = [[UIImageView alloc] initWithImage: image];
self.navigationItem.titleView = imageView;
[imageView release];</textarea>&nbsp;

参考资料：http://stackoverflow.com/questions/844416/how-to-display-an-image-in-the-navigation-bar-of-an-iphone-application

            <div>
                作者：wherejaly 发表于2010/5/12 14:51:00 [原文链接](http://blog.csdn.net/wherejaly/article/details/5582684)
            </div>
            <div>
            阅读：2937 评论：0 [查看评论](http://blog.csdn.net/wherejaly/article/details/5582684#comments)
            </div>