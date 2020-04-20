# Android之如何解决ANR问题

#### ANR产生的原因主要是开发人员使用不当引起的，那么如何避免ANR呢

1. 运行在主线程里的任何方法都尽可能少做事情。

   **特别注意**：Activity应该在它的关键生命周期方法（如onCreate()和onResume()）里尽可能少的去做创建操作。（可以采用重新开启子线程的方式，然后使用Handler+Message的方式做一些操作，比如更新主线程中的ui等）

2. 应用程序应该避免在BroadcastReceiver里做耗时的操作或计算。

   **特别注意**：不要在子线程里做这些任务（因为 BroadcastReceiver的生命周期短），替代的是，如果响应Intent广播需要执行一个耗时的动作的话，应用程序应该启动一个 Service。（此处需要注意的是可以在广播接受者中启动Service，但是却不可以在Service中启动broadcasereciver,关于原因后续会有介绍，此处不是本文重点）

3. 避免在Intent Receiver里启动一个Activity，因为它会创建一个新的画面，并从当前用户正在运行的程序上抢夺焦点。如果你的应用程序在响应Intent广 播时需要向用户展示什么，你应该使用Notification Manager来实现。

