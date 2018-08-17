### MVC
	
* **Model**
 
1. 模型对象: 封装特定于应用程序的数据，并定义操作和处理该数据的逻辑和计算。
	
2. 通信：视图层中用于创建或修改数据的用户操作通过控制器对象进行通信，从而创建或更新模型对象。当模型对象发生更改时（例如，通过网络连接接收新数据），它会通知控制器对象，该对象会更新相应的视图对象。
	
3. 模型对象中不要引用UIKit，即视图对象
 
* **View**
 
1. 视图对象 ：是用户可以看到的应用程序中的对象
	
2. 通信：试图对象通过应用程序的控制器来对模型数据对象完成更改（例如，在文本字段中输入的文本 - 通过控制器对象 - 传递到应用程序的模型对象。
3. 视图对象不应该直接引用Model

* **Controller**
 
1. 控制器对象 ：控制器对象充当应用程序的一个或多个视图对象与其一个或多个模型对象之间的中介。因此，控制器对象是视图对象通过其获知模型对象的变化的通道，反之亦然。控制器对象还可以为应用程序执行设置和协调任务，并管理其他对象的生命周期

2. 通信：控制器对象解释在视图对象中进行的用户操作，并将新的或更改的数据传递给模型层。当模型对象发生更改时，控制器对象会将新模型数据传递给视图对象，以便它们可以显示它
 
* 注意： tableview 和 collectionview 代理方法放在控制器，不然返回cell代理方法数据需要引用model

### MVVM
* **ViewModel**

1. 简化控制器，Controller是app的“胶水代码”，协调模型和视图之间的所有交互。控制器负责管理他们所拥有的视图的视图层次结构，还要响应视图的loading、appearing、disappearing等等，同时往往也会充满我们不愿暴露的model的模型逻辑以及不愿暴露给视图的业务逻辑

2. 视图view仍然不能直接引用模型model，当然controller也不能。相反，他们引用视图模型view model

3. view model是一个放置用户输入验证逻辑，视图显示逻辑，发起网络请求和其他各种各样的代码的极好的地方。有一件事情不应归入view model，那就是任何视图本身的引用。view model的概念同时适用于于iOS和OS X。（换句话说，不要在view model中使用 #import UIKit.h）

4. Controller拥有ViewModel对象，viewmodel通过绑定model更新 View通过绑定ViewModel更新（双向绑定）


### 参考文档
[苹果官方文档释义MVC](https://developer.apple.com/library/archive/documentation/General/Conceptual/DevPedia-CocoaCore/MVC.html#//apple_ref/doc/uid/TP40008195-CH32-SW3)

[猿题库 iOS 客户端架构设计](http://gracelancy.com/blog/2016/01/06/ape-ios-arch-design/)

[Model-View-ViewModel for iOS ](https://www.cnblogs.com/brycezhang/p/3840567.html)

[更轻的视图控制器](https://www.objc.io/issues/1-view-controllers/lighter-view-controllers/)