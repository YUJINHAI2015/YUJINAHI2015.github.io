
---
title:  Runtime-消息调用(第二篇)
date: 2020-05-16 20:52:34
tags:
categories: runtime
---
## Runtime 动态类型

> 在运行程序的时候决定对象的类型

### 什么是动态类型

- 静态类型：`Atom *myAtom;`  -- 在编译的时候检查类型
- 动态类型：`id *myAtom;`  -- 在运行时决定类型

也可以当做参数传递：`- (NSInteger)computeValue:(id<NSdecimalNumberBehaviors>)parameter;`



### 动态绑定

> 在运行程序时将消息和方法对应起来，一般和动态类型一起使用。

```objective-c
@interface Atom : NSObject
- (void)logInfo;
@end
  
// 继承
@interface Hydrogen : Atom
- (void)logInfo;
@end 
  
// 使用
id atom = [Hydrogen alloc] init];
[atom logInfo];

```

调用过程：`[atom logInfo];`

1、确定消息接收器的类型（动态绑定）

2、确定实现的方法（动态绑定）

3、如果找不到，继续在父类中寻找。



### 动态方法的决议

> 不实现方法，只实现函数，然后手动为选择器实现方法。
>
> 可以在运行时给类添加方法
>
> 具体使用场景：比如你有一个方法在很多地方都用到，突然有改动，怎么办，可以通过动态协议在这里拦截他的实现方式，

- 以动态方式实现方法

  通过`resolveInstanceMethod:`和`resolveClassMethod:`能够分别一动态的方式指定实例和类方法选择器的实现代码。

```objective-c
+ (BOOL)resolveInstanceMethod:(SEL)sel {
    
    NSString *method = NSStringFromSelector(sel);
    if ([method hasPrefix:@"absoluteValue"]) {
        class_addMethod([self class], sel, (IMP)absoluteValue, "@@:@");
        NSLog(@"%@",method);
        return YES;
    }
    
    return [super resolveInstanceMethod:sel];
}

id absoluteValue(id self, SEL _cmd, id value) {
    NSInteger inVal = [value integerValue];
    return [NSNumber numberWithInteger:inVal + 10];
}

```



```objective-c
#pragma clang diagnostic push
#pragma clang diagnostic ignored "-Warc-performSelector-leaks"
    Calculator *cal = [[Calculator alloc] init];    
		// 以动态方式创建选择器
    SEL selector1 = NSSelectorFromString(@"absoluteValue:");
    id value = [cal performSelector:selector1 withObject:@(20)];
    NSLog(@"%@",value);
#pragma clang diagnostic pop

```



### 动态加载

> 根据需要加载可执行代码和源代码，而无需在启动时就加载程序的所有组件。
>
> 包bundle机制



### 内省

1、判断是Calculator类的实例还是其子类的实例

`BOOL isCalculator =[myObject isKindOfClass:[Calculator class]];`

2、判断该对象是否实现或继承了能够对该消息作出相应。

`BOOL responds = [myObject respondsToSelector:@selector(sumAddend::)];`

3、是否遵循了该协议

`BOOL conforms = [myObject conformsToProtocol:@protocol(MyProtocol)];`

4、提取方法签名

`NSMethodSignature *signature = [myObject methodSignatureForSelector:@selector(sumAddend::)];`

