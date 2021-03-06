# Local Broadcast Manager

类似EventBus的一个官方工具类。

区别于EventBus，有以下几点：

1. 注册的是Broadcast Receiver；EventBus注册的可以是任意类，只要有用subscribe注解了的公开方法即可。EventBus方便，但由于EventBus是通过反射来找到对应的方法的，所以EventBus在初次注册（因为只要注册过就会以.class为key把相关的方法给存下来，后面再注册时不用再调反射）时会比较耗资源。
2. 消息只能是Intent，而且使用Intent Filter来判断匹配；EventBus的消息则是任意类，使用类名来判断匹配。EventBus方便，但消息类的数量很容易爆炸性增长。
3. 接收方的onReceive方法必然是运行在UI线程的；EventBus则可以在接收方法的注解里标明想要执行的线程，可以是UI线程、工作线程、post消息的调用方所处线程或者异步线程这四个中的任意一个。EventBus更方便。
4. 单例的获取是直接加锁一次判空来构造实例化的；EventBus则是使用了Double Lock Check机制配合volatile关键字来构造实例化的。EventBus在频繁调用时资源耗费比较低。
5. 不支持sticky的消息；EventBus支持sticky的消息。