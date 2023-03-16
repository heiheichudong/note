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
+ gcroot 可达性
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
+ [参看](https://blog.csdn.net/qq_44543508/article/details/103232007)
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
+ 第一次启动：onCreate->onStart->onResume；
+ 打开新的Activity或者返回桌面：onPause->onStop。如果打开新的Activity为透明主题，则不会调用onStop；
+ 当回到原来Activity时：onRestart->onStart->onResume;
+ 当按下返回键：onPause->onStop->onDestroy
+ 横竖屏切换：onPause->onStop->onSaveInstanceState->onDestroy->onCreate->onStart->onRestoreInstanceState->onResume
+ 设置android:configChanges=“orientation|screenSize” onConfigurationChanged 
+ 启动方式
  + standard 默认启动
  + singleTop 在栈顶则不需要重新创建
  + singleTask 将task内的对应Activity实例之上的所有Activity弹出栈
  + singleInstance 新建栈创建activity
> Service
+ startService启动
+ bindService启动
+ [参考](https://blog.csdn.net/amin_hui/article/details/123406301)

