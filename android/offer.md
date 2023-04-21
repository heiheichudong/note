##java
> 面向过程
- 就是字面意思 按步骤实现一个功能
- 优点:
  - 流程化使得编程任务明确，在开发之前基本考虑了实现方式和最终结果，具体步骤清楚，便于节点分析。  
    效率高，面向过程强调代码的短小精悍，善于结合数据结构来开发高效率的程序。
- 缺点：
  - 需要深入的思考，耗费精力，代码重用性低，扩展能力差，后期维护难度比较大。
> 面向对象
- 通过对于具有相同属性和函数方法的一类事物的描述,实现代码功能
- 三大特征
  - 封装：封装就是隐藏对象的属性和实现细节，仅对外公开接口，控制在程序中属性的读和修改的访问级别，  
  将抽象得到的数据和行为（或功能）相结合，形成一个有机的整体，也就是将数据与操作数据的源代码进行有机的结合，  
  形成“类”， 其中数据和函数都是类的成员。
  - 继承：继承是面向对象的基本特征之一，继承机制允许创建分等级层次的类。  
  继承就是子类继承父类的特征和行为，使得子类对象（实例）具有父类的实例域和方法，或子类从父类继承方法，使得子类具有父类相同的行为。
  - 多态：多态同一个行为具有多个不同表现形式或形态的能力。是指一个类实例（对象）的相同方法在不同情形有不同表现形式。  
  多态机制使具有不同内部结构的对象可以共享相同的外部接口。  
  这意味着，虽然针对不同对象的具体操作不同，但通过一个公共的类，它们（那些操作）可以通过相同的方式予以调用。
- 优点：
  - 结构清晰，程序是模块化和结构化，更加符合人类的思维方式；  
    易扩展，代码重用率高，可继承，可覆盖，可以设计出低耦合的系统；  
    易维护，系统低耦合的特点有利于减少程序的后期维护工作量。  
- 缺点：
  - 因为类调用时需要实例化，开销比较大，比较消耗资源，性能比面向过程低。
> 堆栈 gc 内存泄露
+ 堆：堆内存是java内存中的一种，它的作用是用于存储java中的对象和数组。
+ 栈：栈内存是Java的另一种内存，主要是用来执行程序用的。
+ [参考](https://zhuanlan.zhihu.com/p/529280783)
> gc
+ GC 是垃圾回收器的简称，全称是Garbage Collection。
+ gcroot 
+ 可达性
> 四大引用
+ 强引用 > 软引用 > 软引用 > 虚引用
+ 强引用：强引用是最普遍的引用，一般把一个对象赋给一个引用变量，这个引用变量就是强引用。Object obj = new Object();
  + 在一个方法的内部有一个强引用，这个引用（obj）保存在Java栈中，而真正的引用内容(Object)保存在Java堆中。
  + 如果一个对象具有强引用，垃圾回收器不会回收该对象，当内存空间不足时，JVM 宁愿抛出 OutOfMemoryError异常。
  + 如果强引用对象不使用时，需要弱化从而使GC能够回收，如下：obj = null
+ 软引用：是一种相对强引用弱化了一些的引用，需要用java.lang.ref.SoftReference 类来实现。
  ```
      String str=new String("abc");
      SoftReference<String> softRef=new SoftReference<String>(str);
  ```
  + 如果一个对象只具有软引用，则内存空间足够，垃圾回收器就不会回收它，如果内存空间不足了，就会回收这些对象的内存。
+ 弱引用
  ```
  MikeChen mikechen = new MikeChen();
  WeakReference<MikeChen> wr = new WeakReference<MikeChen>(mikechen );
  ```
  + 如果一个对象只具有软引用，则内存空间足够，垃圾回收器就不会回收它，如果内存空间不足了，就会回收这些对象的内存。
  + 弱引用的特点是不管内存是否足够，只要发生 GC，都会被回收
+ 虚引用
  + 虚引用”顾名思义，就是形同虚设，与其他几种引用都不同，虚引用并不会决定对象的生命周期。如果一个对象仅持有虚引用，那么它就和没有任何引用一样，在任何时候都可能被垃圾回收器回收。
  ```
  A a = new A();
  ReferenceQueue<A> rq = new ReferenceQueue<A>();
  PhantomReference<A> prA = new PhantomReference<A>(a, rq);
  ```
> 内存泄露
+ 定义：当不再需要使用的对象，因为不正确使用时，可能导致GC无法回收这些对象。
+ 原因：
  - 对象生命周期变长引发内存泄漏
  - 不关闭资源引发内存泄漏
  - 改变对象哈希值引发内存泄漏
  - 缓存引发内存泄漏
  - [参考](https://juejin.cn/post/7204680573121134652)
> 序列化
+ 把对象转换字节流储存
+ transient修饰字段不被序列化
+ static修饰字段不被序列化
+ [参考](https://blog.csdn.net/qq_44543508/article/details/103232007)
> hash
+ 一般翻译为散列，音译“哈希”。把任意输入通过散列算法变换成固定长度的输出，该输出就是散列值。
+ 哈希会发生碰撞即两个不同的输入值，根据同一散列函数计算出的散列值相同的现象叫做碰撞
+ [参考](https://blog.csdn.net/majinggogogo/article/details/80260400)
> MVC MVP MVVM
+ 为了view与model的解耦
+ mvc 
  + model:数据模型 数据处理
  + view：视图
  + controller:控制器解析view的行为
  + view与model解耦不彻底
+ mvp
  + model:数据模型 数据处理
  + view：视图
  + presenter:用接口去调度view行为和model数据处理
  + view与model解耦彻底
+ mvvm
  + model:数据模型 数据处理
  + view：视图
  + viewModel:用于view与model的数据流向的绑定
  + view与model解耦彻底
##Android
> activity
+ [生命周期](./image/activty.jpg)
+ 第一次启动：onCreate->onStart->onResume;
+ 打开新的Activity或者返回桌面：onPause->onStop。如果打开新的Activity为透明主题，则不会调用onStop;
+ 当回到原来Activity时：onRestart->onStart->onResume;
+ 当按下返回键：onPause->onStop->onDestroy
+ 横竖屏切换：onPause->onStop->onSaveInstanceState->onDestroy->onCreate->onStart->onRestoreInstanceState->onResume
+ 设置android:configChanges=“orientation|screenSize” onConfigurationChanged 
+ 启动方式
  + standard 默认启动
  + singleTop 在栈顶则不需要重新创建
    + 使用场景：登录页面、WXPayEntryActivity、WXEntryActivity 、推送通知栏
  + singleTask 
    + 如果在任务栈中若不存在Activity实例则创建实例；否则则通过onNewIntent激活重用，再重用该实例的时候，会将该实例上的其他activity的实例清除
    + 在对应的任务栈中有且只有一个实例
    + 当然如果和taskAffinity配合使用，则可以在开启或者复用另外任务栈中来创建或者重用Activity实例
    + 有该Activity启动的其他Activity默认都在该Activity所在的任务栈中，除非设置了taskAffinity或者将Activity的launchMode设置为singleInstance
    + 使用场景：程序模块逻辑入口:主页面（Fragment的containerActivity）、WebView页面、扫一扫页面、电商中：购物界面，确认订单界面，付款界面
  + singleInstance
    + 在新的任务栈中开启，并且该新的任务中有且仅有这一个Activity实例，若复用Activity实例时，则通过onNewIntent进行激活。
    + 有该Activity启动的其他Activity不会在该Activity所在的任务栈中，可以在已有的任务栈中，也可以在新创建的任务中。
    + 并且该Activity实例是在整个系统中有且仅有一个。
    + 使用场景：系统Launcher、锁屏键、来电显示等系统应用
+ [参考](https://blog.csdn.net/nihaomabmt/article/details/86490090)
+ [参考](https://blog.csdn.net/black_bird_cn/article/details/79764794)
> Service
- 运行在主线程中，不能做长时间的耗时操作。
+ startService启动
+ bindService启动
+ [参考](https://blog.csdn.net/amin_hui/article/details/123406301)
> RecycleView
+ [参考](https://www.cnblogs.com/jimuzz/p/14040674.html#:~:text=%E5%86%8D%E4%B9%9F%E4%B8%8D%E7%94%A8%E6%8B%85%E5%BF%83%E9%97%AERecycleView%E4%BA%86%E2%80%94%E2%80%94%E9%9D%A2%E8%AF%95%E7%9C%9F%E9%A2%98%E8%AF%A6%E8%A7%A3%201%20%E8%AE%B2%E4%B8%80%E4%B8%8B%20RecyclerView%20%E7%9A%84%E7%BC%93%E5%AD%98%E6%9C%BA%E5%88%B6%2C%E6%BB%91%E5%8A%A810%E4%B8%AA%EF%BC%8C%E5%86%8D%E6%BB%91%E5%9B%9E%E5%8E%BB%EF%BC%8C%E4%BC%9A%E6%9C%89%E5%87%A0%E4%B8%AA%E6%89%A7%E8%A1%8C%20onBindView%20%E3%80%82%20%E7%BC%93%E5%AD%98%E7%9A%84%E6%98%AF%E4%BB%80%E4%B9%88%EF%BC%9F,%E5%90%97%2CnotifyItemChange%E6%96%B9%E6%B3%95%E4%B8%AD%E7%9A%84%E5%8F%82%E6%95%B0%EF%BC%9F%204%20RecyclerView%20%E5%B5%8C%E5%A5%97%20RecyclerView%20%E6%BB%91%E5%8A%A8%E5%86%B2%E7%AA%81%EF%BC%8CNestScrollView%E5%B5%8C%E5%A5%97RecyclerView%E3%80%82%205%20%E8%AF%B4%E8%AF%B4RecyclerView%E6%80%A7%E8%83%BD%E4%BC%98%E5%8C%96%E3%80%82)
> view绘制
+ [参考](https://juejin.cn/post/6844904042175397902)
> 事件分发
+ [参考](https://zhuanlan.zhihu.com/p/144480486)
