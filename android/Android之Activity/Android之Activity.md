# Android之Activity

###### [Android之Activity的爱恨情仇](https://blog.csdn.net/github_34402358/article/details/88168795)

- ###### Android的四大组件是什么？

  Activity：界面让用户操作

  Service ：在后台执行长时间运行操作

  Broadcast Receiver ：运用在应用程序之间传输信息的机制，通过发送Intent来传送我们的数据

  Content Provider ：内容提供者，它是用在不同的应用程序之间共享数据时，可以把一个应用的数据提供给其他的应用使用。

-  Activity的启动模式

   standard、singleTop、singleTask、singleInstance

   **standard**：默认模式，每次启动都会创建一个新的Activity对象，放到目标任务栈的栈顶
   **singleTop**：判断当前的任务栈顶是否存在相同的Activity，如果存在，直接使用，如果不存在，创建一个新的  Activity对象放入栈顶
   **singleTask**：单例模式你，在任务栈中判断是否存在相同的Activity，如果存在，那么会清楚该Activity之上的 所有Activity对象显示，
   如果不存在，创建一个新的Activity对象放入栈顶
   **singleInstance**：会在一个新的任务栈中创建Activity，并且该任务栈中只允许存在一个Activity实例。

- 如何将一个 **Activity** 设置成窗口的样式？

   ​       `android:theme="@android:style/Theme.Dialog"`

- ###### Android中的 **Context**, **Activity**,**Appliction** 有什么区别？

  **相同**:Activity 和 Application 都是 Context 的子类。
  Context 从字面上理解就是上下文的意思,在实际应用中它也确实是起到了管理 上下文环境中各个参数和变量的总用,方便我们可以简单的访问到各种资源。

  **不同**:维护的生命周期不同。Context 维护的是当前的 Activity 的生命周期, Application 维护的是整个项目的生命周期。

