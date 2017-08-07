# RxJava2.0

## Android RxJava第一弹之原理详解、使用详解、常用场景（基于Rxjava2.0）
http://blog.csdn.net/qq_28195645/article/details/52564494

## 关于 RxJava 最友好的文章—— RxJava 2.0 全新来袭
http://www.jianshu.com/p/220955eefc1f

## 手把手教你使用 RxJava 2.0
* 手把手教你使用 RxJava 2.0（一）
http://www.jianshu.com/p/d149043d103a
* 手把手教你使用 RxJava 2.0（二）
http://www.jianshu.com/p/310726a75045
* 手把手教你使用 RxJava 2.0（三）
http://www.jianshu.com/p/1f4867ce3c01


## 这可能是最好的RxJava 2.x入门教程系列专栏
* 这可能是最好的RxJava 2.x 入门教程（一）
http://www.jianshu.com/p/a93c79e9f689
* 这可能是最好的RxJava 2.x 入门教程（二）
http://www.jianshu.com/p/b39afa92807e
* 这可能是最好的RxJava 2.x 入门教程（三）
http://www.jianshu.com/p/e9c79eacc8e3
* 这可能是最好的RxJava 2.x 入门教程（四）
http://www.jianshu.com/p/c08bfc58f4b6
* 这可能是最好的RxJava 2.x 入门教程（五）
http://www.jianshu.com/p/81fac37430dd
* 这可能是最好的RxJava 2.x 教程（完结版）
http://www.jianshu.com/p/0cd258eecf60
* GitHub 代码同步更新
https://github.com/nanchen2251/RxJava2Examples
* RxJava2 Examples —— 这可能是从 RxJava1 跳到 RxJava2（学习 RxJava2 ）最好的例子 Demo
https://github.com/nanchen2251/RxJava2Examples

## 实例应用
* 基于RxJava打造的下载工具, 支持多线程和断点续传
https://www.ctolib.com/RxDownload.html
* Leopard：基于Retrofit+RxJava网络框架
https://www.ctolib.com/YuanClouds-Leopard.html <br>
https://github.com/YuanClouds/SimpleLeopard


## RxJAVA2.0使用环境
先添加Gradle配置:
		
		compile 'io.reactivex.rxjava2:rxjava:2.0.1'
    	compile 'io.reactivex.rxjava2:rxandroid:2.0.1'

## JAVA中的观察者模式原理
在Java中通过  **Observable类** 和 **Observer接口**实现了观察者模式。

* 一个是类  **Observable类**
* 一个是接口 **Observer接口** <br>
* 详细描述：<br> 一个**Observer对象**（观察者）监视着**一个Observable对象**（被观察着）的变化
当**Observable对象**发生变化时，**Observer**得到通知，就可以进行相应的工作。 
这里**Observable（被观察者）**对象的变化是采用**注册(Register)**或者称为**订阅(Subscribe)**的方式告诉**Observer（观察者）**。 <br>
* 逻辑结构
**Observable（被观察者）** --> **订阅(Subscribe)** -->
**Observer（观察者）**

## RxJava的观察者模式原理
* RxJava 有四个基本概念：
	1. Observable (可观察者，即被观察者)、
	2. Observer (观察者)、 
	3. subscribe (订阅)、
	4. 事件。
* 逻辑关系： <br>
  **Observable** 和 **Observer** 通过 **subscribe()** 方法实现订阅关系，从而 **Observable** 可以在需要的时候发出事件来通知 **Observer**。
* 与传统JAVA观察者模式不同：<br>
   **RxJava 的事件** 回调方法除了普通事件 **onNext()** （相当于 **onClick()** / **onEvent()**）之外，还定义了两个特殊的事件：**onCompleted()** 和 **onError()**。
* 三个主要回调方法：
	1. onNext()：**事件发生时** 回调方法
	2. onCompleted(): **事件队列完结** 回调方法 <br>
	   RxJava 不仅把每个事件单独处理，还会**把它们看做一个队列**。**RxJava 规定，当不会再有新的 onNext() 发出时，需要触发 onCompleted() 方法作为标志**。
	3. onError(): **事件队列异常** 回调方法 <br>
	在事件处理过程中出异常时，**onError() 会被触发，同时队列自动终止，不允许再有事件发出**。 
	4. RxJava2.0还添加了一个新的回调方法：**onSubscribe()**，这是为了解决RxJava1.0的backpressure问题，后面会讲到
* RxJava2.0出现了两种观察者模式
	1. Observable(被观察者)/Observer（观察者）不支持背压
	2. Flowable(被观察者)/Subscriber(观察者) 支持背压
* 其他观察者模式
	1. Single/SingleObserver
	2. Completable/CompletableObserver
	3. Maybe/MaybeObserver
	4. 其实这三者都差不多，Maybe/MaybeObserver可以说是前两者的复合体，因此以Maybe/MaybeObserver为例简单介绍一下这种观察者模式的用法
## 背压问题 Observable（被观察着）/Observer（观察者）
* 背压是指在异步场景中，被观察者发送事件速度远快于观察者的处理速度的情况下，一种告诉上游的被观察者降低发送速度的策略
* 不支持背压：当被观察者快速发送大量数据时，下游不会做其他处理，即使数据大量堆积，调用链也不会报MissingBackpressureException,消耗内存过大只会OOM
* 在1.0中，关于背压最大的遗憾，就是集中在Observable这个类中，导致有的Observable支持背压，有的不支持。为了解决这种缺憾，新版本把支持背压和不支持背压的Observable区分开来。






























## RxJAVA2.0原理
首先，用两根水管代替观察者和被观察者，先假设有两根水管：

![GitHub set up](https://github.com/volley5566/AndroidDOC/blob/master/images/1008453-7133ff9a13dd9a59.png?raw=true)

上面一根水管为事件产生的水管，叫它上游吧，下面一根水管为事件接收的水管叫它下游吧。

两根水管通过一定的方式连接起来，使得上游每产生一个事件，下游就能收到该事件。


这里的上游和下游就分别对应着RxJava中的 `Observable` 和`Observer`，它们之间的连接就对应着`subscribe()`，因此这个关系用RxJava来表示就是：

		//创建一个上游 Observable：
        Observable<Integer> observable = Observable.create(new ObservableOnSubscribe<Integer>() {
            @Override
            public void subscribe(ObservableEmitter<Integer> emitter) throws Exception {
                emitter.onNext(1);
                emitter.onNext(2);
                emitter.onNext(3);
                emitter.onComplete();
            }
        });
        //创建一个下游 Observer
        Observer<Integer> observer = new Observer<Integer>() {
            @Override
            public void onSubscribe(Disposable d) {
                Log.d(TAG, "subscribe");
            }

            @Override
            public void onNext(Integer value) {
                Log.d(TAG, "" + value);
            }

            @Override
            public void onError(Throwable e) {
                Log.d(TAG, "error");
            }

            @Override
            public void onComplete() {
                Log.d(TAG, "complete");
            }
        };
        //建立连接
        observable.subscribe(observer);



注意: 只有当上游和下游建立连接之后, 上游才会开始发送事件. 也就是调用了subscribe() 方法之后才开始发送事件.

把这段代码连起来写就成了RxJava引以为傲的链式操作：

		  Observable.create(new ObservableOnSubscribe<Integer>() {
            @Override
            public void subscribe(ObservableEmitter<Integer> emitter) throws Exception {
                emitter.onNext(1);
                emitter.onNext(2);
                emitter.onNext(3);
                emitter.onComplete();
            }
        }).subscribe(new Observer<Integer>() {
            @Override
            public void onSubscribe(Disposable d) {
                Log.d(TAG, "subscribe");
            }

            @Override
            public void onNext(Integer value) {
                Log.d(TAG, "" + value);
            }

            @Override
            public void onError(Throwable e) {
                Log.d(TAG, "error");
            }

            @Override
            public void onComplete() {
                Log.d(TAG, "complete");
            }
        });


*********************
接下来解释一下其中两个陌生的玩意：ObservableEmitter和Disposable.

ObservableEmitter： Emitter是发射器的意思，那就很好猜了，这个就是用来发出事件的，它可以发出三种类型的事件，通过调用emitter的onNext(T value)、onComplete()和onError(Throwable error)就可以分别发出next事件、complete事件和error事件。

* 发射事件，需要满足一定的规则：

```
1. 上游可以发送无限个onNext, 下游也可以接收无限个onNext.
2. 当上游发送了一个onComplete后, 上游onComplete之后的事件将会继续发送, 而下游收到onComplete事件之后将不再继续接收事件.
3. 当上游发送了一个onError后, 上游onError之后的事件将继续发送, 而下游收到onError事件之后将不再继续接收事件.
4. 上游可以不发送onComplete或onError.
5. 最为关键的是onComplete和onError必须唯一并且互斥, 即不能发多个onComplete, 也不能发多个onError, 也不能先发一个onComplete, 然后再发一个onError, 反之亦然

```

注: 关于onComplete和onError唯一并且互斥这一点, 是需要自行在代码中进行控制, 如果你的代码逻辑中违背了这个规则, 并不一定会导致程序崩溃. 比如发送多个onComplete是可以正常运行的, 依然是收到第一个onComplete就不再接收了, 但若是发送多个onError, 则收到第二个onError事件会导致程序会崩溃.