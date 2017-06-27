# RxJava2.0

## RxJAVA2.0使用环境
先添加Gradle配置:
		
		compile 'io.reactivex.rxjava2:rxjava:2.0.1'
    	compile 'io.reactivex.rxjava2:rxandroid:2.0.1'


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