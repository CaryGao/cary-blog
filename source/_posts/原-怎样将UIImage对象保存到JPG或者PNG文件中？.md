---
title: '[原]怎样将UIImage对象保存到JPG或者PNG文件中？'
tags: []
date: 2010-04-28 11:54:00
---

我们都知道如果要从data中或者file中读取数据并包装成UIImage可以使用+ imageWithData:&nbsp;和+&nbsp;imageWithContentsOfFile: 但如果想把UIImage的图片数据写入到jpg或者png格式的文件中呢？答案是UIImageJPEGRepresentation，请看如下代码

<textarea cols="50" rows="15" name="code" class="cpp">/ Create paths to output images
NSString  *pngPath = [NSHomeDirectory() stringByAppendingPathComponent:@"Documents/Test.png"];
NSString  *jpgPath = [NSHomeDirectory() stringByAppendingPathComponent:@"Documents/Test.jpg"];

// Write a UIImage to JPEG with minimum compression (best quality)
// The value 'image' must be a UIImage object
// The value '1.0' represents image compression quality as value from 0.0 to 1.0
[UIImageJPEGRepresentation(image, 1.0) writeToFile:jpgPath atomically:YES];

// Write image to PNG
[UIImagePNGRepresentation(image) writeToFile:pngPath atomically:YES];

// Let's check to see if files were successfully written...

// Create file manager
NSError *error;
NSFileManager *fileMgr = [NSFileManager defaultManager];

// Point to Document directory
NSString *documentsDirectory = [NSHomeDirectory() stringByAppendingPathComponent:@"Documents"];

// Write out the contents of home directory to console
NSLog(@"Documents directory: %@", [fileMgr contentsOfDirectoryAtPath:documentsDirectory error:&amp;error]);</textarea>&nbsp;

参考资料：http://iphonedevelopertips.com/data-file-management/save-uiimage-object-as-a-png-or-jpeg-file.html

            <div>
                作者：wherejaly 发表于2010/4/28 11:54:00 [原文链接](http://blog.csdn.net/wherejaly/article/details/5538248)
            </div>
            <div>
            阅读：14139 评论：1 [查看评论](http://blog.csdn.net/wherejaly/article/details/5538248#comments)
            </div>