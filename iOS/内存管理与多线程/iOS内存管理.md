
---
title: iOS内存管理
date: 2018-3-30
tags: [iOS,内存管理,ARC]
categories: iOS
---
<!--# 内存管理
在编译选项中，为MRC的程序添加-fno-objc-arc标记，表明在编译时，该文件使用MRC编译
如果要在MRC项目中添加ARC的文件，可以使用 -fobjc-arc 标记即可
-->
## Objective-C提供了两种应用程序内存管理方法。
一 OC的内存管理方式有两种，MRR manual retain-release/ MRC manual reference counting（iOS5之前）和ARC automatic reference counting：

1. MRC／MRR是自己“手动保留释放”，跟踪拥有的对象来显式管理内存。通过引用计数的模型实现。

2. 在自动引用计数或ARC中，系统使用与MRC相同的引用计数系统，但它会在编译时插入适当的内存管理方法调用。

二 良好的做法可以防止与内存相关的问题，内存管理不正确会导致两种主要问题：

1. 释放或覆盖仍在使用的数据，这会导致内存损坏，并且通常会导致应用程序崩溃，甚至导致用户数据损坏。

2. 不释放不再使用的数据会导致内存泄漏，内存泄漏是分配的内存不被释放的地方，即使它不再被使用。泄漏导致您的应用程序使用不断增加的内存量，这反过来可能导致系统性能下降或应用程序终止。

从引用计数的角度考虑内存管理通常会适得其反，往往会根据实现细节而不是实际目标来考虑内存管理。相反，应该从对象所有权和对象图的角度考虑内存管理。

## 如何判断当前文件是MRC,还是ARC

1. dealloc能否调用super,只有MRC才能调用super，ARC不要显示的调用dealloc

2. ARC不能使用retain／release／retainCount／autorelease

3. 使用@autoreleasepool块代替NSAutoreleasePool

4. ARC不能使用NSZone


## 自动释放池
NSAutorelesePool对象的生命周期相当于C语言变量的作用域，对于所有调用过autorelease实例方法的对象，在废弃NSAutoreleasePool对象时，都将调用release。
	
	//ios5.0新方式
	@autoreleasepool{
	
	}
	//ios5.0之前的老方式
	NSAutoreleasePool *pool=[[NSAutoreleasePool alloc]init];
	
	[pool drain];
	
	//延迟释放
	NSAutoreleasePool *pool=[[NSAutoreleasePool alloc]init];
	
	id obj = [[NSObject alloc] init];
	[obj autorelease];
	
	[pool drain];//到这里的时候，对象obj会调用release
	
明确什么对象会自动加入 autoreleasepool ：

1. MRC 下需要对象调用 autorelease 才会入池, ARC 下可以通过 __autoreleasing 修饰符，否则的话看方法名，通过调用 alloc/new/copy/mutablecopy 以外的方法取得的对象，编译器帮我们自动加入 autoreleasepool (使用 alloc/new/copy/mutablecopy 方法进行初始化时，由系统管理对象，在适当的位置 release，不加入 autoreleasepool )。
2. 使用 array 会自动将返回对象注册到 autoreleasepool。
3. __weak 修饰的对象，为了保证在引用时不被废弃，会注册到 autoreleasepool 中。
4. id 的指针或对象的指针，在没有显式指定时会被注册到 autoreleasepool 中。

有三种情况您可以使用自己的自动释放池块：

1. 如果您正在编写不基于UI框架的程序，如AppKit等Cocoa框架时,例如命令行工具。
2. 如果你编写一个创建许多临时对象的循环。您可以在循环中使用自动释放池块来在下一次迭代之前处理这些对象。在循环中使用自动释放池块有助于减少应用程序的最大内存占用量。
3. 如果你产生了一个辅助线程，一旦线程开始执行，您必须创建自己的自动释放池块; 否则，你的应用程序会泄漏对象。（有关详细信息，请参阅自动释放池块和线程。）


## 实例：
在Cocoa框架中，相当于程序主循环的NSRunloop或者在其他程序可运行的地方，对NSAutoreleasePool对象的生成，持有和销毁。在没有手加Autorelease Pool的情况下，Autorelease对象是在当前的runloop迭代结束时释放的，而它能够释放的原因是系统在每个runloop迭代中都加入了自动释放池Push和Pop

Autoreleased 对象保持存在的时间超过你想要的。自动释放池会在每个 UI 事件(例如点 击一个按钮)之后清空，但是如果你的事件处理器做了很多处理，例如在一个循环中创建了 很多对象，你可以使用你自己的自动释放池阻止你的应用内存泄漏:

	for (int i = 0; i < 10000 ; i++) {		@autoreleasepool {			NSString *s = [NSString stringWithFormat:. . .]; 
		}
	}


## ARC变量限定符（对象所有权）
* __strong是默认值。只要有一个强有力的指针，一个对象就保持“活着”。
* __weak指定不保持被引用对象活动的引用。当没有强引用时，弱引用被设置为nil。
* __unsafe _ unretained指定一个引用，该引用不会使引用的对象保持活动状态，并且在没有对该对象的强引用时不会设置为nil。如果它所引用的对象被解除分配，指针就会悬空。
* __autoreleasing 用于表示引用（id *）传递的参数，并在返回时自动释放。
	

## 注意
1. ARC也有一些缺点，对于初学者来说，可能仅只能将ARC用在objective-c对象上(也即继承自NSObject的对象)，但是如果涉及到较为底层的东西，比如Core Foundation中的malloc()或者free()等，ARC就鞭长莫及了，这时候还是需要自己手动进行内存管理。

2. 不管是MRC还是ARC管理内存，在项目上架前，一定要对App进行多次测试，比如内存占用，内存泄漏，性能优化等都是值得关注的地方，Xcode的instrument很强大，还有iOS10引进的Debugging Improvements，以及一些自动化测试的第三方库MLeaksFinder等等

## 参考文档
[过渡到ARC发行说明](https://developer.apple.com/library/content/releasenotes/ObjectiveC/RN-TransitioningToARC/Introduction/Introduction.html)

[高级内存管理编程指南](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/MemoryMgmt/Articles/MemoryMgmt.html#//apple_ref/doc/uid/10000011i) 

[Core Foundation的内存管理编程指南](https://developer.apple.com/library/content/documentation/CoreFoundation/Conceptual/CFMemoryMgmt/CFMemoryMgmt.html#//apple_ref/doc/uid/10000127i)

[深入理解 Autorelease](https://juejin.im/post/5a66e28c6fb9a01cbf387da1)

[NSAutoreleasePool](https://developer.apple.com/documentation/foundation/nsautoreleasepool#1651513?language=objc)

[黑幕背后的Autorelease](http://blog.sunnyxx.com/2014/10/15/behind-autorelease/)
