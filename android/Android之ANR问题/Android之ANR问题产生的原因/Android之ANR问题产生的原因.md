# Android之ANR问题产生的原因

#### ANR：Application Not Responding

ANR：它的意思是应用程序未响应。一般出现这种情况，可能是由于我们打开了很多应用程序，占用了大量的内存，或者CPU时间片被一个应用程序长时间占用，不够分配，导致部分应用程序出现了无响应。

**产生ANR（Application not response）这种情况原因是什么？** 

Android中, App的响应能力是由Activity Manager和Window Manager系统服务来监控的，通常情况下产生ANR有三个条件。

1. （UI线程）主线程才会产生ANR
2.   发生某些输入事件或特定操作，比如按键或触屏等输入事件，在BroadcastReceiver或Service的各个生命周期调用函数。
3. 事件响应超时，不同的context规定的上限时间不同

具体表现：

1. 在5秒内没有响应输入的事件（例如，按键按下，屏幕触摸）
2. BroadcastReceiver在10秒内没有执行完毕
3. service是20秒内没有执行完毕