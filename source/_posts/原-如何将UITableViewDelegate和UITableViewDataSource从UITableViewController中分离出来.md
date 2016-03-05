---
title: '如何将UITableViewDelegate和UITableViewDataSource从UITableViewController中分离出来?'
categories:
- objectiveC
tags: 
- objective-c
- ios
- iphone
date: 2010-08-18 16:21:00
---

大家都知道如果给`UITableViewController`装载一些数据和控制cell的行为(高度,样式等)都需要指定`UITableView`的delegate给自身,一般会使用IB或者在`viewDidLoad`中写上`self.tableView.delegate = self;`然后实现`UITableViewDelegate`和`UITableViewDataSource`中的方法,例如:`-tableView:cellForRowAtIndexPath:` 等等.
那么如何将实现`UITableViewDelegate`和`UITableViewDataSource`的方法脱离出来单独放在一个新的class中呢?
<!-- more -->

## 第一步:建立TableDataDelegate

**TableDataDelegate.h**

```objc
@interface TableDataDelegate : NSObject<UITableViewDelegate,UITableViewDataSource> {  
    NSArray *_data;//用于cell的数据,你可以选择自己的方式  
}  
@property (nonatomic,retain) NSArray *data;  
@end  
```

**TableDataDelegate.m**

```objc
#import "TableDataSource.h"
@implementation TableDataSource
@synthesize data = data;
- (CGFloat)tableView:(UITableView *)tableView heightForRowAtIndexPath:(NSIndexPath *)indexPath{
	.......
}
- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath{
	.......
}
- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section{
	......
}
-(void) dealloc{
	[data release];
	[super dealloc];
}
@end
```

该delegate实现了我们需要的方法

**myTableController.h**

```objc
#import "TableDataDelegate.h"
@interface MyTableController : UIViewController {
	UITableView *_tableView;
	TableDataDelegate *_dataDelegate;
}
@property (nonatomic,retain) IBOutlet UITableView *tableView;
@property (nonatomic,retain) IBOutlet TableDataDelegate *dataDelegate;
@end
```

在MyTableController中,我定义了TableDataDelegate这个class,这是必须的,因为这里必须retain它,否则你会运行失败,接下来还需要将它连接到XIB中.

**myTableController.m**

```objc
-(void) viewDidLoad{
 //_dataDelegate.data = ...可以在这里设置你的data,也可以在其他地方,例如viewWillAppear
}
```

## 第二步:在IB中建立连接

![](http://hi.csdn.net/attachment/201008/18/0_12821186343wku.gif)

如上图所示,从Library中拖出Object到我们的XIB中,将class设置为TableDataDelegate,然后将MyTableController中的dataDelegate连接到这里,这一步很重要,我最开始的失败就差了这一步.然后对应的dataSource和delegate都连接到你的UITableView上.

![](http://hi.csdn.net/attachment/201008/18/0_1282118893v1v9.gif)

**UITableView的连接示例**

![](http://hi.csdn.net/attachment/201008/18/0_12821192182WH7.gif)

最后是MyTableController的连接示例

