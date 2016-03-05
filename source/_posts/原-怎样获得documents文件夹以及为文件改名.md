---
title: '[原]怎样获得documents文件夹以及为文件改名'
tags: []
date: 2010-04-26 15:29:00
---

&nbsp;&nbsp;可以使用c函数NSSearchPathForDirectoriesInDomain来查找各种目录。它是Foundation函数，因此它可以与Cocoa for Mac OS X共享。它的很多可用选项都是专门为OS X设计的，在iphone上不会返回任何值。其原因在于，这些位置并不存在于iphone（如Downloads文件夹）上，或者你的应用程序由于iPhone的沙盒机制而没有访问该位置的权限。

<textarea cols="50" rows="15" name="code" class="cpp">	NSArray *paths = NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES);
	NSString *documentsDirectory = [paths objectAtIndex:0];</textarea>&nbsp;

常量NSDocumentDirectory表明我们正在查找Documents目录的路径。第二个常量NSUserDomaininMask表明我们希望将搜索限制于我们应用程序的沙盒。

&nbsp;&nbsp; &nbsp;如果你需要更改一个文件的文件名，你可能会查找NSFileManager的API，但你发现该死的API里根本没有改名的方法，但我们肯定会要应用到改名的操作。其实苹果很狡诈，在movePath方法中是可以用来改名的。

<textarea cols="50" rows="15" name="code" class="c-sharp">NSString *newPath = [[oldPath stringByDeletingLastPathComponent] stringByAppendingPathComponent:newFilename];
[[NSFileManager defaultManager] movePath:oldPath toPath:newPath handler:nil];</textarea>&nbsp;

newFilename是你新文件名，只需要把老文件写入到这个新文件中即完成了改名。。。。。

            <div>
                作者：wherejaly 发表于2010/4/26 15:29:00 [原文链接](http://blog.csdn.net/wherejaly/article/details/5530090)
            </div>
            <div>
            阅读：1933 评论：0 [查看评论](http://blog.csdn.net/wherejaly/article/details/5530090#comments)
            </div>