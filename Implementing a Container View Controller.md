# Implementing a Container View Controller

A custom UIViewController subclass can also act as a container view controller 
 
(一个自定义的ViewController子类可以同时扮演Container ViewController).  

A container view controller manages the presentation of content of other view controllers it owns, also known as its child view controllers 

(每个Container ViewController 管理这里自己ChildViewController内容的呈现).  

A child's view can be presented as-is or in conjunction with views owned by the container view controller.
Your container view controller subclass should declare a public interface to associate its children 

(你的ContainerViewController应该申明自己和ChildViewController之间的管理).  

The nature of these methods is up to you and depends on the semantics of the container you are creating. 

You need to decide how many children can be displayed by your view controller at once, when those children are displayed, and where they appear in your view controller's view hierarchy 

你必须决定你的ContainerViewController一次要显示多少子ChildViewController, 并且这些ChildViewController的View 在哪里显示？.  

Your view controller class defines what relationships, if any, are shared by the children 

你的ContainerViewController定义了你的ChildViewController之间有什么联系.


By establishing a clean public interface for your container, you ensure that children use its capabilities logically, without accessing too many private details about how your container implements the behavior.

通过清晰确定你的ContainerViewController的公共接口，你可以确定你的childViewcontroller不用关系到太多你的ContainerViewController的行为


Your container view controller must associate a child view controller with itself before adding the child's root view to the view hierarchy. 

你的ContainerViewController必须在“把ChildViewCOntroller的RootView加入到自己的View层级”之前，就连接好自己和ChildViewController直接的管理
 
This allows iOS to properly route events to child view controllers and the views those controllers manage. 

通过这样iOS系统就可以合适的追踪子ViewContoller的事件。

Likewise, after it removes a child's root view from its view hierarchy, it should disconnect that child view controller from itself. 

同样的，当一个ChildViewConroller的RootView从他的View层级中移掉时， 他也会取消和ChildViewController之间的关联。

To make or break these associations, your container calls specific methods defined by the base class. These methods are not intended to be called by clients of your container class; 

为了取消这种关联，你的Container要调用基类特殊的方法， 这些方法应该不会被你的Container的客户们调用。

they are to be used only by your container's implementation to provide the expected containment behavior.

他们只能被你的Container实现， 用来提供符合需求的容器行为。

Here are the essential methods you might need to call:


