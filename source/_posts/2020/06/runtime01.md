---
title:  Runtime-消息调用(第一篇)
date: 2020-05-16 19:52:34
tags:
categories: runtime
---

# Runtime-消息调用

> **在运行的时候`确定类型`和`方法解析`**



> 疑问：给对象发送一条消息，如何通过这条消息绑定对应的方法，也就是动态绑定的过程。
>
> 1、通过消息选择器找到对应的选择器类型，也就是 SEL类型
>
> 2、通过消息参数和返回值，确定它的方法签名
>
> 3、通过运行时系统的obj_send方法，传入SEL类型和方法签名，从而调用该消息。
>
> 4、运行时系统会通过传入的参数去找对应的类方法缓存和虚函数表，也就是要找到函数的地址IMP.

### 对象消息和方法

```objective-c
// 方法声明
- (void)sendMessage:(NSString *)arg1 para:(NSString *)arg2;
// 调用方法
[self sendMessage:arg1 para:arg2];
```

{% asset_img image-20200516155533929.png output %}

> > 这条消息传递的表达式中我们能够获取到信息有：

1、接收器（对象或类）：是消息的目的地。

2、消息：由选择器和参数构成

3、选择器：文本字符串

4、实现过程：消息会丢给接收器处理，但是如果该方法没有实现，接收器就会抛出异常，可以通过（对象内省和消息转发）处理。



> > 提出疑问：为什么这样写，就能够调用里面的方法呢？消息怎么找到他的方法的呢？是如何动态绑定的呢？

1、选择器：是一种文本字符：`sendMessage:para:`

2、SEL类型：选择器的类型， 

​        2.1、在编译阶段获取选择器 `SEL myMethod = @selector(sendMessage:para:);`

​        2.2、在运行时阶段获取选择器 `NSSelectorFromString(@"sendMessage:para:");`

​        2.3、为什么要把选择器变成SEL类型呢？因为Objective-C运行时系统只能通过SEL类型传参，调用对应的方法。`self performSelector:...`

3、方法签名：定义了方法输入参数的数据类型和方法的返回值。（数据类型和返回值）



4、[接收器  消息];

```objective-c
// 当我们调用者条语句时
[self sendMessage:arg1 para:arg2];
// 编译器会自动转换成下面这个C函数,要输入的参数有：接收器，选择器类型，参数（方法签名）。
// 上面的语句我们可以获取到：接收器和选择器类型，但是参数（方法签名）要怎么获取呢？
// 系统会通过**方法声明**去猜测方法签名。
void sendMessage(id self, SEL _cmd, id value){

}
```



// 代码实现

```objective-c
#import <Foundation/Foundation.h>

NS_ASSUME_NONNULL_BEGIN

@interface Calculator : NSObject

- (void)sendMessage:(NSString *)arg1 para:(NSString *)arg2;

@end

NS_ASSUME_NONNULL_END
```

```objective-c
#import "Calculator.h"

@implementation Calculator

- (void)sendMessage:(NSString *)arg1 para:(NSString *)arg2 {
    NSLog(@"%@-%@",arg1,arg2);
}
@end

```

// 调用

```objective-c
#import "ViewController.h"
#import "Calculator.h"

@interface ViewController ()

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    // Do any additional setup after loading the view.
#pragma clang diagnostic push
#pragma clang diagnostic ignored "-Warc-performSelector-leaks"
    Calculator *cal = [[Calculator alloc] init];
    SEL selector = @selector(sendMessage:para:);
    [cal performSelector:selector withObject:@"hello1" withObject:@"hello2"];
#pragma clang diagnostic pop
}

// 输出
// 2020-05-16 16:56:30.032136+0800 RuntimeDemo[31818:5784611] hello1-hello2
@end

```

