# Android 8.0新特性

### [官网Android 8.0新特性](https://developer.android.google.cn/about/versions/oreo/android-8.0)

用户体验

通知

在 Android 8.0 中，我们已重新设计通知，以便为管理通知行为和设置提供更轻松和更统一的方式。这些变更包括：

- ![Android 8.0 中的通知长按菜单。](https://developer.android.google.cn/about/versions/oreo/images/notification-long-press.png)

- **图 1.** 用户可以长按应用启动器图标以查看 Android 8.0 中的通知。

- 通知渠道：Android 8.0 引入了通知渠道，其允许您为要显示的每种通知类型创建用户可自定义的渠道。用户界面将通知渠道称之为通知类别。要了解如何实现通知渠道的信息，请参阅[通知渠道](https://developer.android.google.cn/preview/features/notification-channels)指南。
- 通知标志：Android 8.0 引入了对在应用启动器图标上显示通知标志的支持。通知标志可反映某个应用是否存在与其关联、并且用户尚未予以清除也未对其采取行动的通知。通知标志也称为通知点。要了解如何调整通知标志，请参阅[通知标志](https://developer.android.google.cn/preview/features/notification-badges)指南。
- 休眠：用户可以将通知置于休眠状态，以便稍后重新显示它。重新显示时通知的重要程度与首次显示时相同。应用可以移除或更新已休眠的通知，但更新休眠的通知并不会使其重新显示。
- 通知超时：现在，使用 `setTimeoutAfter()` 创建通知时您可以设置超时。您可以使用此函数指定一个持续时间，超过该持续时间后，通知应取消。如果需要，您可以在指定的超时持续时间之前取消通知。
- 通知设置：当您使用 `Notification.INTENT_CATEGORY_NOTIFICATION_PREFERENCES`Intent 从通知创建指向应用通知设置的链接时，您可以调用 `setSettingsText()` 来设置要显示的文本。此系统可以提供以下 Extra 数据和 Intent，用于过滤应用必须向用户显示的设置：`EXTRA_CHANNEL_ID`、`NOTIFICATION_TAG` 和 `NOTIFICATION_ID`。
- 通知清除：系统现在可区分通知是由用户清除，还是由应用移除。要查看清除通知的方式，您应实现 `NotificationListenerService` 类的新 `onNotificationRemoved()` 函数。
- 背景颜色：您现在可以设置和启用通知的背景颜色。只能在用户必须一眼就能看到的持续任务的通知中使用此功能。例如，您可以为与驾车路线或正在进行的通话有关的通知设置背景颜色。您还可以使用 `Notification.Builder.setColor()` 设置所需的背景颜色。这样做将允许您使用 `Notification.Builder.setColorized()` 启用通知的背景颜色设置。
- 消息样式：现在，使用 `MessagingStyle` 类的通知可在其折叠形式中显示更多内容。对于与消息有关的通知，您应使用 `MessagingStyle` 类。您还可以使用新的 `addHistoricMessage()` 函数，通过向与消息相关的通知添加历史消息为会话提供上下文。

自动填充框架

帐号创建、登录和信用卡交易需要时间并且容易出错。在使用要求执行此类重复性任务的应用时，用户很容易遭受挫折。

Android 8.0 通过引入自动填充框架，简化了登录和信用卡表单之类表单的填写工作。在用户选择接受自动填充之后，新老应用都可使用自动填充框架。

您可以采取某些措施，优化您的应用使用此框架的方式。如需了解详细信息，请参阅[自动填充框架概览](https://developer.android.google.cn/preview/features/autofill)。

画中画模式

Android 8.0 允许以画中画 (PIP) 模式启动操作组件。PIP 是一种特殊的多窗口模式，最常用于视频播放。目前，PIP 模式可用于 Android TV，而 Android 8.0 则让该功能可进一步用于其他 Android 设备。

当某个 Activity 处于 PIP 模式时，它会处于暂停状态，但仍应继续显示内容。因此，您应确保您的应用在 `onPause()` 处理程序中进行处理时不会暂停播放。相反，您应在 `onStop()` 中暂停播放视频，并在 `onStart()` 中继续播放。如需了解详细信息，请参阅[多窗口生命周期](https://developer.android.google.cn/guide/topics/ui/multi-window#lifecycle)。

要指定您的 Activity 可以使用 PIP 模式，请在清单中将 `android:supportsPictureInPicture` 设置为 true。（从 Android 8.0 开始，如果您打算在 Android TV 或其他 Android 设备上支持 PIP 模式，则无需将 `android:resizeableActivity` 设置为 true；只有在您的 Activity 支持其他多窗口模式时，才需要设置 `android:resizeableActivity`。）

API 变更

Android 8.0 引入一种新的对象 `PictureInPictureParams`，您可以将该对象传递给 PIP 函数来指定某个 Activity 在其处于 PIP 模式时的行为。此对象还指定了各种属性，例如操作组件的首选纵横比。

现在，在[添加画中画](https://developer.android.google.cn/training/tv/playback/picture-in-picture)中介绍的现有 PIP 函数可用于所有 Android 设备，而不仅限于 Android TV。此外，Android 8.0 还提供以下函数来支持 PIP 模式：

- ```
  Activity.enterPictureInPictureMode(PictureInPictureParams args)
  ```

  ：将操作组件置于画中画模式。操作组件的纵横比和其他配置设置均由

   

  args

   

  指定。如果

   

  args

   

  中的任何字段为空，系统将使用您上次调用

   

  ```
  Activity.setPictureInPictureParams()
  ```

   

  时所设置的值。

  指定的操作组件被置于屏幕的一角，屏幕剩余部分则被屏幕显示的上一个操作组件填满。进入 PIP 模式的 Activity 将进入暂停状态，但仍保持已启动状态。如果用户点按此 PIP 操作组件，系统将显示一个菜单供用户操作，而在操作组件处于 PIP 状态期间，不会理会任何触摸事件。

- `Activity.setPictureInPictureParams()`：更新操作组件的 PIP 配置设置。如果操作组件目前处于 PIP 模式，则会更新此设置；如果操作组件的纵横比发生变化，这非常有用。如果操作组件不处于 PIP 模式，则会使用这些配置设置，而不会考虑您调用的 `enterPictureInPictureMode()` 函数。

可下载字体

Android 8.0 和 Android 支持库 26 允许您从提供程序应用请求字体，而无需将字体绑定到 APK 中或让 APK 下载字体。此功能可减小 APK 大小，提高应用安装成功率，使多个应用可以共享同一种字体。

如需了解有关下载字体的详细信息，请参阅 [可下载字体](https://developer.android.google.cn/preview/features/downloadable-fonts)。

XML 中的字体

Android 8.0 推出一项新功能，即 XML 中的字体，允许您使用字体作为资源。这意味着，不再需要以资产的形式捆绑字体。字体在 `R` 文件中编译，并且作为一种资源，可自动用于系统。然后，您可以利用一种新的资源类型 `font` 来访问这些字体。

在运行 API 版本 14 及更高版本的设备中，支持库 26 对此功能提供完全支持。

如需了解有关以资源形式使用字体以及检索系统字体有关的详细信息，请参阅 [XML 中的字体](https://developer.android.google.cn/preview/features/fonts-in-xml)。

自动调整 TextView 的大小

Android 8.0 允许您根据 TextView 的大小自动设置文本展开或收缩的大小。这意味着，在不同屏幕上优化文本大小或者优化包含动态内容的文本大小比以往简单多了。如需了解有关如何在 Android 8.0 中自动调整 TextView 的大小的详细信息，请参阅[自动调整 TextView 的大小](https://developer.android.google.cn/preview/features/autosizing-textview)。



自适应图标

Android 8.0 引入自适应启动器图标。自适应图标支持视觉效果，可在不同设备型号上显示为各种不同的形状。要了解如何创建自适应图标，请参阅[自适应图标](https://developer.android.google.cn/preview/features/adaptive-icons)预览功能指南。

颜色管理

图像应用的 Android 开发者现在可以利用支持广色域彩色显示的新设备。要显示广色域图像，应用需要在其清单（每个操作组件）中启用一个标志，并加载具有嵌入的广域彩色配置文件（AdobeRGB、Pro Photo RGB、DCI-P3 等）的位图。

WebView API

Android 8.0 提供多种 API，帮助您管理在应用中显示网页内容的 `WebView` 对象。这些 API 可增强应用的稳定性和安全性，它们包括：

- Version API
- Google SafeBrowsing API
- Termination Handle API
- Renderer Importance API

要详细了解如何这些 API，请参阅[管理 WebView](https://developer.android.google.cn/preview/features/managing-webview)。

固定快捷方式和小部件

Android 8.0 引入了快捷方式和微件的应用内固定功能。在您的应用中，您可以根据用户权限为支持的启动器创建固定的快捷方式和小部件。

如需了解详细信息，请参阅[固定快捷方式和微件](https://developer.android.google.cn/preview/features/pinning-shortcuts-widgets)预览功能指南。

最大屏幕纵横比

以 Android 7.1（API 级别 25）或更低版本为目标平台的应用默认的最大屏幕纵横比为 1.86。针对 Android 8.0 或更高版本的应用没有默认的最大纵横比。如果您的应用需要设置最大纵横比，请使用定义您的操作组件的清单文件中的 [maxAspectRatio](https://developer.android.google.cn/reference/android/R.attr#maxAspectRatio) 属性。 

多显示器支持

从 Android 8.0 开始，此平台为多显示器提供增强的支持。如果 Activity 支持多窗口模式，并且在具有多显示器的设备上运行，则用户可以将 Activity 从一个显示器移动到另一个显示器。当应用启动 Activity 时，此应用可指定 Activity 应在哪个显示器上运行。

**注：**如果 Activity 支持多窗口模式，则 Android 8.0 将为该 Activity 自动启用多显示器支持。您应测试您的应用，确保它在多显示器环境下可正常运行。

每次只有一个 Activity 可以处于继续状态，即使此应用具有多个显示器。具有焦点的 Activity 将处于继续状态，所有其他可见的 Activity 均暂停，但不会停止。如需了解有关当多个 Activity 可见时活动生命周期的详细信息，请参阅[多窗口生命周期](https://developer.android.google.cn/guide/topics/ui/multi-window#lifecycle)。

当用户将 Activity 从一个显示器移动到另一个显示器时，系统将调整 Activity 大小，并根据需要发起运行时变更。您的 Activity 可以自行处理配置变更，或允许系统销毁包含该 Activity 的进程，并以新的尺寸重新创建它。如需了解详细信息，请参阅[处理配置变更](https://developer.android.google.cn/guide/topics/resources/runtime-changes)。

`ActivityOptions` 提供两个新函数以支持多个显示器：

- `setLaunchDisplayId()`

  指定 Activity 在启动后应显示在哪个显示器上。

- `getLaunchDisplayId()`

  返回操作组件的当前启动显示器。

对 adb shell 进行了扩展，以支持多个显示器。`shell start` 命令现在可用于启动操作组件，并指定操作组件的目标显示器：

```
adb shell start <activity_name> --display <display_id>
```

统一的布局外边距和内边距

Android 8.0 让您可以更轻松地指定 `View` 元素的对边使用相同外边距和内边距的情形。具体来说，您现在可以在布局 XML 文件中使用以下属性：

- [`layout_marginVertical`](https://developer.android.google.cn/reference/android/R.attr#layout_marginVertical)，同时定义 [`layout_marginTop`](https://developer.android.google.cn/reference/android/R.attr#layout_marginTop) 和 [`layout_marginBottom`](https://developer.android.google.cn/reference/android/R.attr#layout_marginBottom)。
- [`layout_marginHorizontal`](https://developer.android.google.cn/reference/android/R.attr#layout_marginHorizontal)，同时定义 [`layout_marginLeft`](https://developer.android.google.cn/reference/android/R.attr#layout_marginLeft) 和 [`layout_marginRight`](https://developer.android.google.cn/reference/android/R.attr#layout_marginRight)。
- [`paddingVertical`](https://developer.android.google.cn/reference/android/R.attr#paddingVertical)，同时定义 [`paddingTop`](https://developer.android.google.cn/reference/android/R.attr#paddingTop) 和 [`paddingBottom`](https://developer.android.google.cn/reference/android/R.attr#paddingBottom)。
- [`paddingHorizontal`](https://developer.android.google.cn/reference/android/R.attr#paddingHorizontal)，同时定义 [`paddingLeft`](https://developer.android.google.cn/reference/android/R.attr#paddingLeft) 和 [`paddingRight`](https://developer.android.google.cn/reference/android/R.attr#paddingRight)。

**注**：如果您自定义应用逻辑以[支持不同语言和文化](https://developer.android.google.cn/training/basics/supporting-devices/languages)（包括文本方向），请记住，这些属性不会影响 [`layout_marginStart`](https://developer.android.google.cn/reference/android/R.attr#layout_marginStart)、[`layout_marginEnd`](https://developer.android.google.cn/reference/android/R.attr#layout_marginEnd)、[`paddingStart`](https://developer.android.google.cn/reference/android/R.attr#paddingStart) 或 [`paddingEnd`](https://developer.android.google.cn/reference/android/R.attr#paddingEnd) 的值。您可以自行设置这些值和新的垂直与水平布局属性来创建取决于文本方向的布局行为。

指针捕获

某些应用（例如游戏、远程桌面和虚拟化客户端）将大大受益于鼠标指针控制。指针捕获是 Android 8.0 中的一项新功能，可以通过将所有鼠标事件传递到您的应用中焦点视图的方式提供此类控制。

从 Android 8.0 开始，您的应用中的 `View` 可以请求指针捕获并定义一个侦听器来处理捕获的指针事件。鼠标指针在此模式下将隐藏。如果不再需要鼠标信息，该视图可以释放指针捕获。系统也可以在视图丢失焦点时（例如，当用户打开另一个应用时）释放指针捕获。

如需了解有关如何在您的应用中使用此功能的信息，请参阅[指针捕获](https://developer.android.google.cn/preview/features/pointer-capture)。

应用类别

在适当的情况下，Android 8.0 允许每个应用声明其所属的类别。这些类别用于将应用呈现给用户的用途或功能类似的应用归类在一起，例如按流量消耗、电池消耗和存储消耗将应用归类。您可以在 `` 清单标记中设置 `android:appCategory` 属性，定义应用的类别。

Android TV 启动器

Android 8.0 添加了一种以内容为中心的全新 [Android TV 主屏幕体验](https://developer.android.google.cn/preview/features/tvlauncher)，支持 Android TV 模拟器和 Nexus Player Android 8.0 设备映像。新的主屏幕在对应于频道的行中组织视频内容，这些频道在系统上通过应用填充各个节目。应用可以发布多个频道，用户可以配置他们希望在主屏幕上看到哪些频道。Android TV 也包含一个 Watch Next 行，此行根据用户的观看习惯从应用填充节目。应用也可以提供视频预览，这些预览会在用户聚焦到节目时自动播放。用于填充频道和节目的 API 属于 TvProvider API，这些 API 以 Android 支持库模块的形式随 Android 8.0 分发。

AnimatorSet

从 Android 8.0 开始，`AnimatorSet` API 现在支持寻道和倒播功能。寻道功能允许您将动画的位置设置为指定的时间点处。如果您的应用包含可撤消的操作的动画，倒播功能会很有用。现在，您不必定义两组独立的动画，而只需反向播放同一组动画。

输入和导航

键盘导航键区

如果您的应用中，某个操作组件使用一种复杂的视图层次结构（如图 2 所示），可考虑将多组界面元素组成一个键区，简化键盘导航这些元素的操作。用户可以在 Chromebook 设备上按 Meta+Tab 或 Search+Tab，在不同键区之间导航。键区的一些范例包括：侧面板、导航栏、主内容区域和可能包含多个子元素的元素。

![以一个包含五个导航键区的操作组件为例，用户可以使用键盘导航键区快捷键进行导航。键区按以下布局显示：顶部面板、左侧面板、主内容区域、底部面板和浮动操作按钮。](https://developer.android.google.cn/about/versions/oreo/images/keyboard-navigation-clusters.png)**图 2.** 包含 5 个键区的操作组件

要将一个 `View` 或 `ViewGroup` 元素设置为一个键区，请在元素的布局 XML 文件中将 [`android:keyboardNavigationCluster`](https://developer.android.google.cn/reference/android/view/View#attr_android:keyboardNavigationCluster) 属性设置为 `true`，或者将 `true` 传递至应用界面逻辑中的 `setKeyboardNavigationCluster()`。

**注**：键区不能嵌套，不过，非嵌套键区可以显示在层次结构的不同层级。如果您尝试嵌套键区，框架仅会将最顶层的 `ViewGroup` 元素视为键区。

在具有触摸屏的设备中，您可以将某个键区指定的 `ViewGroup` 对象的 `android:touchscreenBlocksFocus` 元素设置为 `true`，仅允许从键区导航进入和离开此键区。如果您将此配置应用于某个键区，用户将无法使用 Tab 键或箭头键导航进入或离开此键区，而是必须按键区导航键盘组合键。

视图默认焦点

在 Android 8.0 中，您可以指定在（重新）创建的操作组件继续运行并且用户按下键盘导航键（例如 Tab 键）之后应接收焦点的 `View`。要应用“设为默认焦点”设置，请在包含界面元素的布局 XML 文件中将 `View` 元素的 [`android:focusedByDefault`](https://developer.android.google.cn/reference/android/view/View#attr_android:focusedByDefault) 属性设置为 `true`，或者将 `true` 传递至应用界面逻辑中的 `setFocusedByDefault()`。

系统

新的 StrictMode 检测程序

Android 8.0 添加了三个新的 StrictMode 检测程序，帮助识别应用可能出现的错误：

- `detectUnbufferedIo()` 将检测您的应用何时读取或写入未缓冲的数据，这可能极大影响性能。
- `detectContentUriWithoutPermission()` 将检测您的应用在其外部启动 Activity 时何时意外忘记向其他应用授予权限。
- `detectUntaggedSockets()` 将检测您的应用何时使用网络流量，而不使用 `setThreadStatsTag(int)` 将流量标记用于调试目的。

缓存数据

Android 8.0 优化了缓存数据的导航和行为。现在，每个应用均获得一定的磁盘空间配额，用于存储 `getCacheQuotaBytes(UUID)` 返回的缓存数据。

当系统需要释放磁盘空间时，将开始从超过配额最多的应用中删除缓存文件。因此，如果将您的缓存数据量始终保持低于配额的水平，则在必须清除系统中的某些文件时，您的缓存文件将能坚持到最后。系统在决定删除您的应用中的哪些缓存文件时，将首先考虑删除最旧的文件（由修改时间确定）。

您还可以针对每个目录启用两种新行为，以控制系统如何释放缓存数据：

- `StorageManager.setCacheBehaviorAtomic()` 可用于指示某个目录及其所有内容应作为一个不可分割的整体进行删除。
- `setCacheBehaviorTombstone(File, boolean)` 可用于指示不应删除某个目录内的文件，而应将它们截断到 0 字节长度，使空文件保持完好。

最后，在需要为大文件分配磁盘空间时，可考虑使用新的 `allocateBytes(FileDescriptor, long)` API，它将自动清除属于其他应用的缓存文件（根据需要），以满足您的请求。在确定设备是否有足够的磁盘空间保存您的新数据时，请调用 `getAllocatableBytes(UUID)` 而不要使用 `getUsableSpace()`，因为前者会考虑系统要为您清除的任何缓存数据。

内容提供程序分页

我们已更新内容提供程序以支持加载大型数据集，每次加载一页。例如，一个具有大量图像的照片应用可查询要在页面中显示的数据的子集。内容提供程序返回的每个结果页面由一个 Cursor 对象表示。客户端和提供程序必须实现分页才能利用此功能。

如需了解有关内容提供程序变更的详细信息，请参阅 `ContentProvider` 和 `ContentProviderClient`。

内容刷新请求

现在，`ContentProvider` 和 `ContentResolver` 类均包含 `refresh()` 函数，这样，客户端可以更轻松地知道所请求的信息是否为最新信息。

您可以扩展 `ContentProvider` 以添加自定义的内容刷新逻辑。请务必重写 `refresh()` 函数，以返回 `true`，告知提供程序的客户端您已尝试自行刷新数据。

您的客户端应用可通过调用另一个函数（又称 `refresh()`），显式请求已刷新的内容。在调用此函数时，传入待刷新数据的 URI。

**注**：由于您可能通过网络不断请求数据，您应仅在有明显迹象表明内容确已过时时才从客户端调用 `refresh()`。执行此类内容刷新最常见的原因是响应[滑动刷新](https://developer.android.google.cn/training/swipe/add-swipe-interface)手势，该手势显式请求当前界面显示最新内容。

JobScheduler 改进

Android 8.0 引入了对 `JobScheduler` 的多项改进。由于您通常可以使用计划作业替代现在受限的后台服务或隐式广播接收器，这些改进可以让您的应用更轻松地符合新的[后台执行限制](https://developer.android.google.cn/preview/features/background)。

`JobScheduler` 的更新包括：

- 您现在可以将工作队列与计划作业关联。要将一个工作项添加到作业的队列中，请调用 [`JobScheduler.enqueue()`](https://developer.android.google.cn/reference/android/app/job/JobScheduler#enqueue(android.app.job.JobInfo, android.app.job.JobWorkItem))。当作业运行时，它可以将待定工作从队列中剥离并进行处理。这种功能可以处理之前需要启动后台服务（尤其是实现 `IntentService` 的服务）的许多用例。

- 您现在可以通过调用 [`JobInfo.Builder.setClipData()`](https://developer.android.google.cn/reference/android/app/job/JobInfo.Builder#setClipData(android.content.ClipData, int)) 的方式将 `ClipData` 与作业关联。利用此选项，您可以将 URI 权限授予与作业关联，类似于这些权限传递到 `Context.startService()` 的方式。您也可以将 URI 权限授予用于工作队列上的 intent。

- 计划作业现在支持多个新的约束条件：

  - [`JobInfo.isRequireStorageNotLow()`](https://developer.android.google.cn/reference/android/app/job/JobInfo#isRequireStorageNotLow())

    如果设备的可用存储空间非常低，作业将不会运行。

  - [`JobInfo.isRequireBatteryNotLow()`](https://developer.android.google.cn/reference/android/app/job/JobInfo#isRequireBatteryNotLow())

    如果电池电量等于或低于临界阈值，作业将不会运行；临界阈值是指设备显示 **Low battery warning** 系统对话框的电量。

  - [`NETWORK_TYPE_METERED`](https://developer.android.google.cn/reference/android/app/job/JobInfo#NETWORK_TYPE_METERED)

    作业需要一个按流量计费的网络连接，比如大多数移动数据网络数据套餐。

自定义数据存储

Android 8.0 允许您为首选项提供自定义数据存储，如果您的应用将首选项存储在云或本地数据库中，或者如果首选项特定于某个设备，此功能会非常有用。如需了解有关实现数据存储的详细信息，请参阅[自定义数据存储](https://developer.android.google.cn/preview/features/custom-data-store)。

findViewById() 签名变更

现在，`findViewById()` 函数的全部实例均返回 ` T`，而不是 `View`。此变更会带来以下影响：

- 例如，如果 `someMethod(View)` 和 `someMethod(TextView)` 均接受调用 `findViewById()` 的结果，这可能导致现有代码的返回类型不确定。
- 在使用 Java 8 源语言时，这需要在返回类型不受限制时（例如，`assertNotNull(findViewById(...)).someViewMethod())`）显式转换为 `View`。
- 重写非最终的 `findViewById()` 函数（例如，`Activity.findViewById()`）将需要更新其返回类型。

媒体增强功能

VolumeShaper

有一个新的 [VolumeShaper](https://developer.android.google.cn/preview/features/volumeshaper) 类。您可以用它来执行简短的自动音量转换，例如淡入、淡出和交叉淡入淡出。

音频焦点增强功能

音频应用通过请求和舍弃音频焦点的方式在设备上共享音频输出。应用通过启动或停止播放或者闪避音量的方式处理处于聚焦状态的变更。有一个新的 `AudioFocusRequest` 类。对于此类，应用在处理音频焦点变化时会使用[新功能](https://developer.android.google.cn/preview/features/audiofocus)：[自动闪避](https://developer.android.google.cn/preview/features/audiofocus#automatic_ducking)和[延迟聚焦](https://developer.android.google.cn/preview/features/audiofocus#delayed_focus_gain)。

媒体指标

新的 `getMetrics()` 函数将返回一个包含配置和性能信息的 `PersistableBundle` 对象，用一个包含属性和值的地图表示。为以下媒体类定义 `getMetrics()` 函数：

- `MediaPlayer.getMetrics()`
- `MediaRecorder.getMetrics()`
- `MediaCodec.getMetrics()`
- `MediaExtractor.getMetrics()`

为每个实例单独收集指标，并持续到实例的生命周期结束为止。如果没有可用的指标，则此函数将返回 null。返回的实际指标取决于类。

MediaPlayer

Android 8.0 为 MediaPlayer 类添加了多种新函数。这些函数可以从多个方面增强您的应用处理媒体播放的能力：

- 在[搜索](https://developer.android.google.cn/preview/features/media-player#seeking)帧时进行精细控制。
- 播放[受数字版权管理保护的](https://developer.android.google.cn/preview/features/media-player#drm)材料的功能。

MediaPlayer 现在支持[采样级加密](https://developer.android.google.cn/preview/features/media-player#sle)。

音频录制器

- 音频录制器现在支持对流式传输有用的 MPEG2_TS 格式：

  ```
  mMediaRecorder.setOutputFormat(MediaRecorder.OutputFormat.MPEG_2_TS);
  ```

  请参阅 `MediaRecorder.OutputFormat`

- `MediaMuxer` 现在可以处理任意数量的音频和视频流，而不再仅限于一个音频曲目和/或一个视频曲目。使用 `addTrack()` 可混录所需的任意数量的曲目。

- `MediaMuxer` 还可以添加一个或多个包含用户定义的每帧信息的元数据曲目。元数据的格式由您的应用定义。仅对 MP4 容器支持元数据曲目。

元数据可以用于离线处理。例如，传感器的陀螺仪信号可以用于执行视频稳定操作。

在添加元数据曲目时，曲目的 MIME 格式必须以前缀“application/”开头。除了数据不是来源于 `MediaCodec` 以外，写入元数据的操作与写入视频/音频数据相同。相反，应用将包含相关时间戳的 `ByteBuffer` 传递给 `writeSampleData()` 函数。时间戳必须和视频及音频曲目处于相同的时基。

生成的 MP4 文件使用 ISOBMFF 的 12.3.3.2 部分定义的 `TextMetaDataSampleEntry`，指示元数据的 MIME 格式。在使用 `MediaExtractor` 提取包含元数据曲目的文件时，元数据的 MIME 格式将提取到 `MediaFormat` 中。

音频播放控制

Android 8.0 允许您查询和请求设备产生声音的方式。对音频播放的以下控制将让您的服务更轻松地仅在有利的设备条件下产生声音。

Google 智能助理的新音频使用类型

`AudioAttributes` 类包含一种新的声音类型，即 `USAGE_ASSISTANT`，对应于 Google 智能助理在设备上的回答。

设备音频播放的变更

如果您希望自己的服务仅在特定的设备音频配置处于活动状态时开始产生声音，您可以使用 `AudioManager` 类注册一个 `AudioManager.AudioPlaybackCallback` 实例，后者的`onPlaybackConfigChanged()` 函数可以帮助您确定当前活动的音频属性集。

显式请求音频焦点

您的服务可以使用 `requestAudioFocus()` 函数提交一个更精细的设备级音频焦点接收请求。传入一个 `AudioFocusRequest` 对象，您可以使用 `AudioFocusRequest.Builder` 创建这个对象。在这个构建类中，您可以指定以下选项：

- 您希望获得的焦点类型，例如 `AUDIOFOCUS_GAIN_TRANSIENT` 或 `AUDIOFOCUS_GAIN_TRANSIENT_MAY_DUCK`。
- 当另一个音频服务获得设备焦点时，您的服务应以更安静的方式继续，还是完全暂停。
- 您的服务能否等待获得焦点，直至设备就绪。

**注**：构建您的 `AudioFocusRequest` 实例时，如果您通过调用 `setAcceptsDelayedFocusGain()` 指示您的服务可以等待产生声音，您也必须调用 `setOnAudioFocusChangeListener()`，以便您的服务了解它何时可以开始产生声音。

增强的媒体文件访问功能

[存储访问框架 (SAF)](https://developer.android.google.cn/guide/topics/providers/document-provider) 允许应用显示自定义 `DocumentsProvider`，后者可以为其他应用提供访问数据源中的文件的权限。事实上，文档提供程序甚至可以提供驻留在网络存储区或使用[媒体传输协议 (MTP)](https://en.wikipedia.org/wiki/Media_Transfer_Protocol) 等协议的文件的访问权限。

但是，访问远程数据源中的大媒体文件面临一些挑战：

- 媒体播放器需要以寻址方式访问来自文档提供程序的文件。当大媒体文件驻留在远程数据源上时，文档提供程序必须事先提取所有数据，并创建快照文件描述符。媒体播放器无法播放没有文件描述符的文件，因此在文档提供程序完成文件下载前，无法开始播放。
- 照片应用等媒体集合管理器必须通过作用域文件夹遍历一系列访问 URI 才能访问存储在外部 SD 卡上的媒体。这种访问模式会让媒体上的批量操作（例如移动、复制和删除）变得非常缓慢。
- 媒体集合管理器无法根据文档的 URI 确定其位置。这就让这些类型的应用难以允许用户选择媒体文件的保存位置。

Android 8.0 通过改进存储访问框架解决了各个挑战。

自定义文档提供程序

从 Android 8.0 开始，存储访问框架允许[自定义文档提供程序](https://developer.android.google.cn/guide/topics/providers/create-document-provider)为驻留在远程数据源中的文件创建可寻址的文件描述符。SAF 可打开文件，获取原生可寻址的文件描述符。然后 SAF 向文档提供程序提交离散字节请求。此功能使文档提供程序可以返回媒体播放器应用请求的准确字节范围，而不必事先缓存整个文件。

要使用此功能，您需要调用新的 `StorageManager.openProxyFileDescriptor()` 函数。`openProxyFileDescriptor()`函数可接受 `ProxyFileDescriptorCallback` 对象作为回调。任何时候，当客户端应用对文档提供程序返回的文件描述符执行文件操作时，SAF 都会调用回调。

直接文档访问

从 Android 8.0 开始，您可以使用 `getDocumentUri()` 函数获得与给定 `mediaUri` 引用相同文档的 URI。不过，由于返回的 URI 由 `DocumentsProvider` 提供支持，媒体集合管理器可以直接访问文档，不用遍历作用域目录树。因此，媒体管理器能够以明显加快的速度对文档执行文件操作。

**注意**：`getDocumentUri()` 函数仅可以定位媒体文件；无法授予应用访问这些文件的权限。要详细了解如何获取媒体文件的访问权限，请参阅参考文档。

文档路径

在 Android 8.0 中使用存储访问框架时，您可以根据文档的 ID，使用 `findDocumentPath()` 函数（存在于 `DocumentsContract` 和 `DocumentsProvider` 类中）从文件系统的根目录中确定路径。该函数将在 `DocumentsContract.Path` 对象中返回此路径。如果文件系统对相同文档有多个定义的路径，该函数将返回访问具有给定 ID 的文档时最常使用的路径。

此功能在下列情况下特别有用：

- 您的应用使用可以显示特定文档位置的“另存为”对话框。
- 您的应用在搜索结果视图中显示文件夹并且如果用户选择某个文件夹，应用必须加载此特定文件夹内的子文档。

**注**：如果您的应用仅具有路径中某些文档的访问权限，那么 `findDocumentPath()` 的返回值将仅包含您的应用可以访问的文件夹和文档。

连接

WLAN 感知

Android 8.0 新增了对 WLAN 感知的支持，此技术基于周边感知联网 (NAN) 规范。在具有相应 WLAN 感知硬件的设备上，应用和附近设备可以通过 WLAN 进行搜索和通信，无需依赖互联网接入点。我们正在与硬件合作伙伴合作，以尽快将 WLAN 感知技术应用于设备。要了解有关如何将 WLAN 感知集成到您的应用中的信息，请参阅 [WLAN 感知](https://developer.android.google.cn/preview/features/wifi-aware)。

蓝牙

Android 8.0 通过增加以下功能，增强了平台对蓝牙的支持：

- 支持 AVRCP 1.4 标准，该标准支持音乐库浏览。
- 支持蓝牙低功耗 (BLE) 5.0 标准。
- 将 Sony LDAC 编解码器集成到蓝牙堆叠中。

配套设备配对

在尝试通过蓝牙、BLE 和 WLAN 与配套设备配对时，Android 8.0 提供的 API 允许您自定义配对请求对话框。如需了解详细信息，请参阅[配套设备配对](https://developer.android.google.cn/preview/features/companion-device-pairing)。

如需了解有关在 Android 上使用蓝牙的详细信息，请参阅[蓝牙](https://developer.android.google.cn/guide/topics/connectivity/bluetooth)指南。有关对蓝牙所作的特定于 Android 8.0 的变更，请参阅 [Android 8.0 行为变更](https://developer.android.google.cn/preview/behavior-changes)页面的[蓝牙](https://developer.android.google.cn/preview/behavior-changes#bt)部分。

共享

智能共享

Android 8.0 了解用户的个性化分享首选项，在通过哪些应用分享各个类型的内容方面，也有着更好的把握。例如，如果用户为一张收据拍照，Android 8.0 可以建议费用跟踪应用；如果用户自拍，一款社交媒体应用可以更好地处理图像。Android 8.0 可以根据用户的个性化首选项自动学习所有这些模式。

智能分享适用于 `image` 之外的内容类型，例如 `audio`、`video`、`text` 和 `URL` 等。

要启用智能分享，请将具有最多三个字符串注释的 `ArrayList` 添加到分享内容的 intent。这些注释应说明内容中的主要部分或主题。下面的代码示例显示了如何向 intent 添加注释：

```
ArrayList<String> annotations = new ArrayList<>();

annotations.add("topic1");
annotations.add("topic2");
annotations.add("topic3");

intent.putStringArrayListExtra(
    Intent.EXTRA_CONTENT_ANNOTATIONS,
    annotations
);
```

如需了解有关智能分享注释的详细信息，请参阅 `EXTRA_CONTENT_ANNOTATIONS`。

智能文本选择

在兼容设备上，Android 8.0 让应用可以帮助用户以更有意义的方式与文本交互。当用户长按某个*实体*中可识别格式的单词（例如某个地址或餐馆名称）时，系统会选中整个实体。用户会看到一个浮动工具栏，该工具栏包含可以处理所选文本实体的应用。例如，如果系统识别出某个地址，它可以将用户导向地图应用。

系统识别的实体包括地址、网址、电话号码和电子邮件地址。如需了解详细信息，请参阅 `TextClassifier`。

无障碍功能

Android 8.0 支持开发者使用以下无障碍功能创建自己的无障碍服务。如需了解有关如何让您的应用更便于访问的更多信息，请参阅[无障碍功能](https://developer.android.google.cn/guide/topics/ui/accessibility)。



无障碍功能按钮

您的无障碍服务现在可以请求在系统的导航区域显示*无障碍功能按钮*，该按钮让用户可从其设备上的任意位置快速激活您的服务功能。要执行此操作，请在某个 `AccessibilityServiceInfo` 对象的 [`android:accessibilityFlags`](https://developer.android.google.cn/reference/android/accessibilityservice/AccessibilityServiceInfo#attr_android:accessibilityFlags) 属性中添加 `FLAG_REQUEST_ACCESSIBILITY_BUTTON` 标志。稍后，您可以使用 `registerAccessibilityButtonCallback()` 注册回调。

**注**：此功能仅适用于提供软件渲染导航区域的设备。请始终使用 `isAccessibilityButtonAvailable()`，并通过实现 `onAvailabilityChanged()` 根据无障碍功能按钮的可用性来响应变更。通过该方式，用户可以始终访问您的服务功能，即使该无障碍功能按钮不受支持或变得不可用。

独立的音量调整

Android 8.0 引入了 `STREAM_ACCESSIBILITY` 音量类别，允许您单独控制无障碍服务音频输出的音量，而不会影响设备上的其他声音。

要使用这个新的流类型来控制无障碍服务音量，请在无障碍服务中设置 `FLAG_ENABLE_ACCESSIBILITY_VOLUME` 选项。然后，您可以使用 `adjustStreamVolume()` 更改设备的无障碍服务音频音量。

指纹手势

您的无障碍服务也可以响应替代的输入机制，即沿设备的指纹传感器按特定方向滑动（上、下、左和右）。要接收有关这些交互的回调，请完成以下一系列步骤：

1. 声明 [`USE_FINGERPRINT`](https://developer.android.google.cn/reference/android/Manifest.permission#USE_FINGERPRINT) 权限和 `CAPABILITY_CAN_REQUEST_FINGERPRINT_GESTURES` 功能。
2. 在 [`android:accessibilityFlags`](https://developer.android.google.cn/reference/android/accessibilityservice/AccessibilityServiceInfo#attr_android:accessibilityFlags) 属性中设置 `FLAG_REQUEST_FINGERPRINT_GESTURES` 标志。
3. 使用 `registerFingerprintGestureCallback()` 注册回调。

请记住，并非所有设备都包含指纹传感器。您可以使用 `isHardwareDetected()` 函数识别设备是否支持此传感器。即使对于包含指纹传感器的设备，您的服务也只有在指纹传感器不用于身份验证目的时才可使用它。要识别此传感器何时可用，请调用 `isGestureDetectionAvailable()` 函数并实现 `onGestureDetectionAvailabilityChanged()` 回调。

字词级突出显示

要确定 `TextView` 对象中可见字符的位置，您可以在 `EXTRA_DATA_TEXT_CHARACTER_LOCATION_KEY` 中将其作为第一个参数传递到 `refreshWithExtraData()` 中。随后会更新您为 `refreshWithExtraData()` 提供的作为第二个参数的 `Bundle`对象，使之包含一个可打包的 `Rect` 对象数组。每个 `Rect` 对象代表某个特定字符的边界框。

如果您的服务使用 `TextToSpeech` 对象朗读屏幕上出现的内容，您可以获取有关文本到语音转换引擎何时开始朗读单个合成字词时的准确时间信息，前提是文本到语音转换引擎提供此信息。当引擎即将开始播放特定范围文本的音频时，Text-to-Speech API 会通知您的服务，将使用 `onRangeStart()` 函数开始朗读此范围的文本。

如果您创建自己的 `TextToSpeechService` 实现，您可以使用 `rangeStart()` 函数支持这一新功能。

标准化单端范围值

`AccessibilityNodeInfo` 的一些实例使用 `AccessibilityNodeInfo.RangeInfo` 的某个实例来表明界面元素可接受一定范围的值。使用 `RangeInfo.obtain()` 创建范围或使用 `getMin()` 和 `getMax()` 检索此范围的极值时，请注意，Android 8.0 规定了标准化单端范围：

- 对于没有最小值的范围，`Float.NEGATIVE_INFINITY` 表示最小值。
- 对于没有最大值的范围，`Float.POSITIVE_INFINITY` 表示最大值。

提示文本

Android 8.0 包含可用于与文本可编辑对象的提示文本进行交互的多个函数：

- `isShowingHintText()` 和 `setShowingHintText()` 函数分别显示和设置节点的当前文本内容是否表示节点的提示文本。如果节点不包含可编辑文本，则它不应包含提示文本。
- 要访问提示文本本身，请使用 `getHintText()`。即使某个对象当前未显示提示文本，系统也能成功调用 `getHintText()`。

连续的手势分派

您的服务现在可以使用 `GestureDescription.StrokeDescription` 构造函数中的最后一个参数 `willContinue`，指定属于同一设定手势的笔划的顺序。

安全性与隐私

权限

Android 8.0 引入了多个与电话有关的新权限：

- [`ANSWER_PHONE_CALLS`](https://developer.android.google.cn/reference/android/Manifest.permission#ANSWER_PHONE_CALLS) 允许您的应用通过编程方式接听呼入电话。要在您的应用中处理呼入电话，您可以使用 `acceptRingingCall()` 函数。
- [`READ_PHONE_NUMBERS`](https://developer.android.google.cn/reference/android/Manifest.permission#READ_PHONE_NUMBERS) 权限允许您的应用读取设备中存储的电话号码。

这些权限均被划分为[危险](https://developer.android.google.cn/guide/topics/permissions/requesting#normal-dangerous)类别，属于 [`PHONE`](https://developer.android.google.cn/reference/android/Manifest.permission_group#PHONE) 权限组。

新的帐号访问和 Discovery API

Android 8.0 对应用访问用户帐号的方式引入多项改进。对于由身份验证器管理的帐号，身份验证器在决定对应用隐藏帐号还是显示帐号时可以使用自己的策略。Android 系统跟踪可以访问特定帐号的应用。

在以前的 Android 版本中，想要跟踪用户帐号列表的应用必须获取有关所有帐号的更新，包括具有不相关类型的帐号。Android 8.0 添加了 `addOnAccountsUpdatedListener(android.accounts.OnAccountsUpdateListener, android.os.Handler, boolean, java.lang.String[])` 函数，其允许应用指定应接收帐号变更的帐号类型列表。

API 变更

AccountManager 提供六个新函数以帮助身份验证器管理哪些应用可以查看某个帐号：

- `setAccountVisibility(android.accounts.Account, java.lang.String, int)`：针对特定用户帐号和软件包组合设置可见性级别。
- `getAccountVisibility(android.accounts.Account, java.lang.String)`：获取特定用户帐号和软件包组合的可见性级别。
- `getAccountsAndVisibilityForPackage(java.lang.String, java.lang.String)`：允许身份验证器获取帐号和给定软件包的可见性级别。
- `getPackagesAndVisibilityForAccount(android.accounts.Account)`：允许身份验证器获取存储的给定帐号的可见性值。
- `addAccountExplicitly(android.accounts.Account, java.lang.String, android.os.Bundle, java.util.Map)`：允许身份验证器初始化帐号的可见性值。
- `addOnAccountsUpdatedListener(android.accounts.OnAccountsUpdateListener, android.os.Handler, boolean, java.lang.String[])`：将 `OnAccountsUpdateListener` 侦听器添加到 `AccountManager` 对象。无论设备上的帐号列表何时发生变化，系统都将调用此侦听器。

Android 8.0 引入两个特殊的软件包名称值，以使用 `setAccountVisibility(android.accounts.Account, java.lang.String, int)` 函数指定未设置的应用的可见性级别。`PACKAGE_NAME_KEY_LEGACY_VISIBLE` 可见性值应用于具有 `GET_ACCOUNTS` 权限的应用，并且其目标 Android 版本低于 Android 8.0，或其签名与针对任意 Android 版本的身份验证器匹配。`PACKAGE_NAME_KEY_LEGACY_NOT_VISIBLE` 为之前未设置的应用提供默认的可见性值，对于此类应用，`PACKAGE_NAME_KEY_LEGACY_VISIBLE` 不适用。

如需了解有关新的帐号访问和发现 API 的详细信息，请参阅 `AccountManager` 和 `OnAccountsUpdateListener` 参考。

Google Safe Browsing API

`WebView` 类现在添加了一个 Safe Browsing API 来增强网络浏览的安全性。如需了解详细信息，请参阅 [Google Safe Browsing API](https://developer.android.google.cn/preview/features/managing-webview#safe-browsing)。

测试

仪器测试

Android 8.0 为应用的仪器测试提供以下几项额外支持。

针对非默认应用进程运行

现在，您可以指定针对您的应用的默认进程以外的进程运行特定仪器测试。如果您的应用包含多个在不同进程中运行的操作组件，此配置非常有用。

要定义非默认进程仪器测试，请导航至您的清单文件，然后导航至所需的 [``](https://developer.android.google.cn/guide/topics/manifest/instrumentation-element) 元素。添加 `android:targetProcess` 属性，并将它的值设置为以下值之一：

- 特定进程的名称。
- 以逗号分隔的进程名称列表。
- 通配符（`"*"`），允许针对任何执行 `android:targetPackage` 属性中指定的软件包中的代码的已启动进程运行仪器测试。

在执行仪器测试时，您可以通过调用 `getProcessName()` 检查正在测试哪个进程。

在测试过程中报告结果

现在，通过调用 `addResults()`，您可以在执行仪器测试时（而不用等到测试后）报告结果。

用于测试的模拟 Intent

为了更轻松地为您应用的操作组件创建隔离、独立的界面测试，Android 8.0 引入了 `onStartActivity()` 函数。要处理您的测试类调用的特定 intent，您可以在 `Instrumentation.ActivityMonitor` 类的自定义子类中替换此函数。

当您的测试类调用 intent 时，该函数将返回一个存根 `Instrumentation.ActivityResult` 对象，而不是执行 intent 本身。通过在您的测试中使用这种模拟 intent 逻辑，您可以侧重于自己的操作组件如何准备和处理您传递到不同操作组件或完全不同的应用中的 intent。

运行时和工具

平台优化

Android 8.0 为平台引入了运行时优化和其他优化，这些优化将带来多项性能改进。这些优化包括并发压缩垃圾回收、更有效的内存利用和代码区域。

它们可以加快启动时间，并为 OS 和应用带来更好的性能。

更新的 Java 支持

Android 8.0 添加了对更多 OpenJDK Java API 的支持：

- OpenJDK 8 中的 `java.time`。
- OpenJDK 7 中的 `java.nio.file` 和 `java.lang.invoke`。

要详细了解这些新添加的软件包中的类和函数，请参阅 API 参考文档。

如果您想要在 Android Studio 中[使用 Java 8 语言功能](https://developer.android.google.cn/studio/preview/features/java8-support)，您应[下载最新的预览版本](https://developer.android.google.cn/studio/preview)。

更新的 ICU4J Android Framework API

Android 8.0 扩展了 [ICU4J Android 框架 API](https://developer.android.google.cn/guide/topics/resources/icu4j-framework)—，它是 ICU4J API 的子集—，供应用开发者在 `android.icu` 软件包中使用。这些 API 使用设备上具有的本地化数据。因此，您无需在 APK 中编译 ICU4J 库，从而减少 APK 占用空间。

**表 1.** Android 中使用的 ICU、CLDR 和 Unicode 版本。

| Android API 级别                                       | ICU 版本 | CLDR 版本 | Unicode 版本 |
| :----------------------------------------------------- | :------- | :-------- | :----------- |
| Android 7.0（API 级别 24），Android 7.1（API 级别 25） | 56       | 28        | 8.0          |
| Android 8.0                                            | 58.2     | 30.0.3    | 9.0          |

如需详细了解针对受支持的 ICU4J API 的更新，请阅读[版本说明](https://developer.android.google.cn/preview/release-notes#icu4j)。 

Android 企业版

已为运行 Android 8.0 的设备引入新的企业功能和 API。重要功能包括如下：

- 完全托管的设备中的工作资料使企业可以在管理工作数据与个人数据的同时，将它们分离开来。
- API 委派允许设备所有者和个人资料所有者将应用管理分配给其他应用。
- 配置流程中的用户体验改进措施（包含新的自定义选项）缩短了设置时间。
- 蓝牙、WLAN、备份和安全性方面的新增控制选项使企业可以更精细地管理设备。网络操作组件日志记录可帮助企业追查问题。