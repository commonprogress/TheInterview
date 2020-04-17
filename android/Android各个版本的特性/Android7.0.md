# Android 7.0新特性

### [Android 7.0官网地址](https://developer.android.google.cn/about/versions/nougat/android-7.0)

- ## 多窗口支持

- ## 通知增强功能

- ## 配置文件指导的 JIT/AOT 编译

- ## 快速的应用安装路径

- ## 随时随地低电耗模式

- ## Project Svelte：后台优化

- ## SurfaceView

- ## 流量节省程序

- ## Vulkan API

- ## Quick Settings Tile API

- ## 号码屏蔽

- ## 来电过滤

- ## 多语言区域支持，更多语言

- ## 新增的表情符号

- ## Android 中的 ICU4J API

- ## WebView

- ### 多进程

- ## APK signature scheme v2

- ## 作用域目录访问

- ## 键盘快捷键辅助工具

- ## 网络安全性配置

多窗口支持

在 Android 7.0 中，我们为该平台引入了一个新的而且非常需要的多任务处理功能 — 多窗口支持。 

现在，用户可以一次在屏幕上打开两个应用。 

- 在运行 Android 7.0 的手机和平板电脑上，用户可以并排运行两个应用，或者处于分屏模式时一个应用位于另一个应用之上。用户可以通过拖动两个应用之间的分隔线来调整应用。 
- 在 Android TV 设备上，应用可以将自身置于[画中画模式](https://developer.android.google.cn/preview/features/picture-in-picture)，从而让它们可以在用户浏览或与其他应用交互时继续显示内容。

![img](https://developer.android.google.cn/images/android-7.0/mw-portrait.png)

**图 1.** 在分屏模式下运行的应用。

多窗口支持为您提供新的吸引用户方式，特别是在平板电脑和其他更大屏幕的设备上。您甚至可以在您的应用中启用拖放，从而使用户可以方便地将内容拖放到您的应用或从其中拖出内容—这是一个非常好的增强用户体验的方式。 

向您的应用添加多窗口支持并配置多窗口显示的处理方式非常简单。例如，您可以指定您的 Activity 允许的最小尺寸，从而防止用户将 Activity 调整到该尺寸以下。您还可以为应用停用多窗口显示，这可确保系统将仅以全屏模式显示应用。

如需了解详细信息，请参阅[多窗口支持](https://developer.android.google.cn/preview/features/multi-window)开发者文档。

通知增强功能

在 Android 7.0 中，我们重新设计了通知，使其更易于使用并且速度更快。部分变更包括：

- **模板更新**：我们正在更新通知模板，新强调了英雄形象和化身。开发者将能够充分利用新模板，只需进行少量的代码调整。
- **消息传递样式自定义**：您可以自定义更多与您的使用 `MessagingStyle`类的通知相关的用户界面标签。您可以配置消息、会话标题和内容视图。
- **捆绑通知**：系统可以将消息组合在一起（例如，按消息主题）并显示组。用户可以适当地进行拒绝或归档等操作。如果您已实现 Android Wear 的通知，那么您已经很熟悉此模式。
- **直接回复**：对于实时通信应用，Android 系统支持内联回复，以便用户可以直接在通知界面中快速回复短信。
- **自定义视图**：两个新的 API 让您在通知中使用自定义视图时可以充分利用系统装饰元素，如通知标题和操作。

![img](https://developer.android.google.cn/images/android-7.0/notifications-1.png)

![img](https://developer.android.google.cn/images/android-7.0/notifications-3.png)

![img](https://developer.android.google.cn/images/android-7.0/notifications-2.png)

**图 2.** 绑定的通知和直接回复。

要了解如何实现新功能的信息，请参阅[通知](https://developer.android.google.cn/preview/features/notification-updates)指南。

配置文件指导的 JIT/AOT 编译

在 Android 7.0 中，我们添加了即时 (JIT) 编译器，对 ART 进行代码分析，让它可以在应用运行时持续提升 Android 应用的性能。JIT 编译器对 Android 运行组件当前的 Ahead of Time (AOT) 编译器进行了补充，有助于提升运行时性能，节省存储空间，加快应用更新和系统更新速度。

配置文件指导的编译让 Android 运行组件能够根据应用的实际使用以及设备上的情况管理每个应用的 AOT/JIT 编译。例如，Android 运行组件维护每个应用热方法的配置文件，并且可以预编译和缓存这些方法以实现最佳性能。对于应用的其他部分，在实际使用之前不会进行编译。

除提升应用的关键部分的性能外，配置文件指导的编译还有助于减少整个 RAM 占用，包括关联的二进制文件。此功能对于低内存设备非常尤其重要。

Android 运行组件在管理配置文件指导的编译时，可最大程度降低对设备电池的影响。仅当设备处于空闲状态和充电时才进行编译，从而可以通过提前执行该工作节约时间和省电。

快速的应用安装路径

Android 运行组件的 JIT 编译器最实际的好处之一是应用安装和系统更新的速度。即使在 Android 6.0 中需要几分钟进行优化和安装的大型应用，现在只需几秒钟就可以完成安装。系统更新也变得更快，因为省去了优化步骤。 

随时随地低电耗模式...

Android 6.0 推出了低电耗模式，即设备处于空闲状态时，通过推迟应用的 CPU 和网络活动以实现省电目的的系统模式，例如，设备放在桌上或抽屉里时。 

现在，在 Android 7.0 中，低电耗模式又前进了一步，随时随地可以省电。只要屏幕关闭了一段时间，且设备未插入电源，低电耗模式就会对应用使用熟悉的 CPU 和网络限制。这意味着用户即使将设备放入口袋里也可以省电。

![img](https://developer.android.google.cn/images/android-7.0/doze-diagram-1.png)

**图 3.** 低电耗模式现在应用限制以延长电池寿命，即使设备未处于静止状态。

屏幕关闭片刻后，设备在使用电池时，低电耗模式将限制网络访问，同时延迟作业和同步。在短暂的维护时间范围后，其允许应用访问网络，并执行延迟的作业/同步。打开屏幕或将设备插入电源会使设备退出低电耗模式。

当设备再次处于静止状态时，屏幕关闭且使用电池一段时间，低电耗模式针对 `PowerManager.WakeLock`、`AlarmManager` 警报和 GPS/WLAN 扫描应用完整 CPU 和网络限制。

无论设备是否处于运动状态，将应用调整到低电耗模式的最佳做法均相同，因此，如果您已更新应用以妥善处理低电耗模式，则一切就绪。如果不是，请立即开始[将应用调整到低电耗模式](https://developer.android.google.cn/training/monitoring-device-state/doze-standby#assessing_your_app)。

Project Svelte：后台优化

Project Svelte 在持续改善，以最大程度减少生态系统中一系列 Android 设备中系统和应用使用的 RAM。在 Android 7.0 中，Project Svelte 注重优化在后台中运行应用的方式。 

后台处理是大多数应用的一个重要部分。处理得当，可让您实现非常棒的用户体验 — 即时、快速和情境感知。如果处理不得当，后台处理会毫无必要地消耗 RAM（和电池），同时影响其他应用的系统性能。 

自 Android 5.0 发布以来，`JobScheduler` 已成为执行后台工作的首选方式，其工作方式有利于用户。应用可以在安排作业的同时允许系统基于内存、电源和连接情况进行优化。JobScheduler 可实现控制和简洁性，我们想要所有应用都使用它。 

另一个非常好的选择是 [`GCMNetworkManager`](https://developers.google.cn/android/reference/com/google/android/gms/gcm/GcmNetworkManager)（Google Play 服务的一部分），其在旧版 Android 中提供类似的作业安排和兼容性。

我们在继续扩展 `JobScheduler` 和 `GCMNetworkManager`，以符合多个用例 — 例如，在 Android 7.0 中，现在，您可以基于内容提供程序中的更改安排后台工作。同时，我们开始弃用一些较旧的模式，这些模式会降低系统性能，特别是低内存设备的系统性能。

在 Android 7.0 中，我们删除了三个常用隐式广播 — `CONNECTIVITY_ACTION`、`ACTION_NEW_PICTURE` 和`ACTION_NEW_VIDEO` — 因为这些广播可能会一次唤醒多个应用的后台进程，同时会耗尽内存和电池。如果您的应用收到这些广播，请充分利用 Android 7.0 以迁移到 `JobScheduler` 和相关的 API。 

如需了解详情，请查看[后台优化](https://developer.android.google.cn/preview/features/background-optimization)文档。

SurfaceView

Android 7.0 可同步移动到 `SurfaceView` 类，此类在某些情况下提供的电池性能优于 `TextureView`：在渲染视频或 3D 内容时，包含滚动和动画视频位置的应用在使用 `SurfaceView` 时比 `TextureView` 耗电更少。

`SurfaceView` 类可减少屏幕合成对电池的消耗，因为它是在专用硬件中合成，与应用窗口内容分隔开。因此，它产生的中间副本少于 `TextureView`。



现在，`SurfaceView` 对象的内容位置和包含的应用内容同步更新。这一变化导致的一个结果是，在画面移动时，`SurfaceView` 中播放的视频的简单的平移或缩放不再在画面侧面产生黑条。

从 Android 7.0 开始，我们强烈建议您使用 `SurfaceView` 代替 `TextureView`，以实现省电。

流量节省程序

![img](https://developer.android.google.cn/images/android-7.0/datasaver.png)

**图 4.** 设置中的流量节省程序

在移动设备的整个生命周期，移动数据网络计划的成本通常会超出设备本身的成本。对于许多用户而言，移动数据网络是他们想要节省的昂贵资源。 

Android 7.0 推出了流量节省模式，这是一项新的系统服务，有助于减少应用使用的移动数据网络，无论是在漫游，账单周期即将结束，还是使用少量的预付费数据包。流量节省程序让用户可以控制应用使用移动数据网络的方式，同时让开发者打开流量节省程序时可以提供更多有效的服务。 

用户在 **Settings** 中启用流量节省程序且设备位于按流量计费的网络上时，系统屏蔽后台流量消耗，同时指示应用在前台尽可能使用较少的流量 — 例如，通过限制用于流媒体服务的比特率、降低图像质量、延迟最佳的预缓冲等方法来实现。用户可以将特定应用加入白名单以允许后台按流量计费的流量消耗，即使在打开流量节省程序时也是如此。

Android 7.0 扩展了 `ConnectivityManager`，以便为应用[检索用户的流量节省程序首选项](https://developer.android.google.cn/preview/features/data-saver#status)并[监控首选项变更](https://developer.android.google.cn/preview/features/data-saver#monitor-changes)提供一种方式。所有应用均应检查用户是否已启用流量节省程序并努力限制前台和后台流量消耗。

Vulkan API

Android 7.0 将一项新的 3D 渲染 API [Vulkan™](http://www.khronos.org/vulkan) 集成到平台中。就像 [OpenGL™ ES](https://www.khronos.org/opengles/) 一样，Vulkan 是 3D 图形和渲染的一项开放标准，由 Khronos Group 维护。

Vulkan 是完全从零开始设计，以最小化驱动器中的 CPU 开销，并能让您的应用更直接地控制 GPU 操作。Vulkan 还允许多个线程同时执行工作，如命令缓冲区构建，以获得更好的并行化。

Vulkan 开发工具和库都已卷入 Android 7.0DK。它们包括：

- 标头
- 验证层（调试库）
- SPIR-V 着色程序编译器
- SPIR-V 运行时着色器编译库

Vulkan 仅适用于已启用 Vulkan 硬件的设备上的应用，如 Nexus 5X、Nexus 6P 和 Nexus Player。我们正在与合作伙伴密切合作，以尽快使 Vulkan 能面向更多的设备。

如需了解详细信息，请参阅 [API 文档](https://developer.android.google.cn/ndk/guides/graphics)。

Quick Settings Tile API

![img](https://developer.android.google.cn/images/android-7.0/quicksettings.png)

**图 5.** 通知栏中的快速设置图块。

“快速设置”通常用于直接从通知栏显示关键设置和操作，非常简单。在 Android 7.0 中，我们已扩展“快速设置”的范围，使其更加有用更方便。 

我们为额外的“快速设置”图块添加了更多空间，用户可以通过向左或向右滑动跨分页的显示区域访问它们。我们还让用户可以控制显示哪些“快速设置”图块以及显示的位置 — 用户可以通过拖放图块来添加或移动图块。 

对于开发者，Android 7.0 还添加了一个新的 API，从而让您可以定义自己的“快速设置”图块，使用户可以轻松访问您应用中的关键控件和操作。

对于急需或频繁使用的控件和操作，保留“快速设置”图块，且不应将其用作启动应用的快捷方式。

定义图块后，您可以将它们显示给用户，用户可通过拖放将图块添加到“快速设置”。

如需了解有关创建应用图块的信息，请参阅可下载的 [API 参考](https://developer.android.google.cn/preview/setup-sdk#docs-dl)中的文件 `android.service.quicksettings.Tile`。

号码屏蔽

Android 7.0 现在支持在平台中进行号码屏蔽，提供框架 API，让服务提供商可以维护屏蔽的号码列表。默认短信应用、默认手机应用和运营商应用可以对屏蔽的号码列表进行读取和写入操作。其他应用则无法访问此列表。

通过使号码屏蔽成为平台的标准功能，Android 为应用提供一致的方式来支持广泛的设备上的号码屏蔽。应用可以利用的其他优势包括：

- 还会屏蔽已屏蔽的来电号码发出的短信 
- 通过 Backup & Restore（备份和还原）功能可以跨重置和设备保留屏蔽的号码 
- 多个应用可以使用相同的屏蔽号码列表

此外，通过 Android 的运营商应用集成表示运营商可以读取设备上屏蔽的号码列表，并为用户执行服务端屏蔽，以阻止不需要的来电和短信通过任何介质（如 VOIP 端点或转接电话）到达用户。

如需了解详细信息，请参阅可下载的 [API 参考](https://developer.android.google.cn/preview/setup-sdk#docs-dl)中的 `android.provider.BlockedNumberContract`。

来电过滤

Android 7.0 允许默认的手机应用过滤来电。手机应用执行此操作的方式是实现新的 `CallScreeningService`，该方法允许手机应用基于来电的 `Call.Details` 执行大量操作，例如：

- 拒绝来电 
- 不允许来电到达通话记录 
- 不向用户显示来电通知

如需了解详细信息，请参阅可下载的 [API 参考](https://developer.android.google.cn/preview/setup-sdk#docs-dl)中的 `android.telecom.CallScreeningService`。

多语言区域支持，更多语言

Android 7.0 现在允许用户在设置中选择**多个语言区域**，以更好地支持双语用例。应用可以使用新的 API 获取用户选择的语言区域，然后为多区域设置用户提供更成熟的用户体验 — 如以多个语言显示搜索结果，并且不会以用户了解的语言翻译网页。

除多语言区域支持外，Android 7.0 还扩展了用户可用的语言范围。它针对常用语言提供超过 25 种的变体，如英语、西班牙语、法语和阿拉伯语。它还针对 100 多种新语言添加了部分支持。

应用可以通过调用 `LocaleList.GetDefault()` 获取用户设置的语言区域列表。为支持扩展的语言区域数量，Android 7.0 正在改变其解析资源的方式。请务必使用新的资源解析逻辑测试和验证您的应用是否能如期运行。

要了解新资源解析行为和应遵循的最佳做法，请参阅[多语言支持](https://developer.android.google.cn/preview/features/multilingual-support)。

新增的表情符号

Android 7.0 引入更多表情符号和表情符号相关功能，包括肤色表情符号和支持变量选择符。如果您的应用支持表情符号，请遵循以下准则，以便能充分利用这些表情符号相关功能优势。

- **在插入之前，检查设备是否包含表情符号。**要检查系统字体中有哪些表情符号，使用 `hasGlyph(String)` 方法。
- **检查表情符号是否支持变量选择符。**变量选择符使您能够呈现一些彩色或黑白的表情符号。在移动设备上，应用应呈现彩色的表情符号，而不是黑白的。但是，如果您的应用显示嵌入在文本中的表情符号，那应使用黑白变量。要确定表情符号是否有变量，使用变量选择符。如需有关支持变量的字符的完整清单，请参阅[变量的 Unicode 文档](http://www.unicode.org/Public/9.0.0/ucd/StandardizedVariants-9.0.0d1.txt)中的*表情符号变量序列*部分。
- **检查表情符号是否支持肤色。**Android 7.0 允许用户按照他们的喜好修改表情符号呈现的肤色。键盘应用应为有多个肤色的表情符号提供可视化的指示，并应允许用户选择他们喜欢的肤色。要确定哪些系统表情符号有肤色修改器，使用 `hasGlyph(String)` 方法。您可以通过读取 [Unicode 文档](http://unicode.org/emoji/charts/full-emoji-list.html)来确定哪些表情符号使用肤色。

Android 中的 ICU4J API

Android 7.0 目前在 Android 框架（位于 `android.icu` 软件包下）中提供 [ICU4J](http://site.icu-project.org/) API 的子集。迁移很简单，主要是需要从 `com.java.icu` 命名空间更改为 `android.icu`。如果您已在您的应用中使用 ICU4J 捆绑包，切换到 Android 框架中提供的 `android.icu` API 可以大量节省 APK 大小。

要详细了解 Android ICU4J API，请参阅 [ICU4J 支持](https://developer.android.google.cn/preview/features/icu4j-framework)。

WebView

Chrome 和 WebView 配合使用

从 Android 7.0 及更高版本中的 Chrome 版本 51 开始，您的设备中的 Chrome APK 用于提供和渲染 Android 系统 WebView。这种方法改善了设备本身的内存使用率，同时减少保持 WebView 更新所需的带宽（因为只要保持启用 Chrome，单机版 WebView APK 将不再进行更新）。

您可以启用开发者选项和选择 **WebView 实现**，选择您的 WebView 提供商。您可以使用设备上安装的任何兼容的 Chrome 版本（Dev、Beta 或 Stable）或单机版 Webview APK，作为 WebView 实现。

多进程

从 Android 7.0 中的 Chrome 版本 51 开始，WebView 将开发者选项“多进程 WebView”被启用时，在一个单独的沙盒进程中运行网页内容。

我们正在寻求关于 N 中的兼容性和运行时性能的反馈，并随后将在未来 Android 版本中启用多进程 WebView。在这个版本中，可预期启动时间回归、总内存使用和软件渲染性能。

如果您在多进程模式中遇到意外问题，请告诉我们。请通过 [Chromium 错误跟踪程序](https://bugs.chromium.org/p/chromium/issues/entry?template=Webview Bugs)联系 WebView 团队。

Javascript 在页面加载之前运行

从以 Android 7.0 为目标平台的应用开始，JavaScript 上下文会在加载新页面时重置。目前，新 WebView 实例中加载的第一个页面会继承上下文。

想要在 WebView 中注入 Javascript 的开发者应在页面开始加载后执行脚本。

不安全起点上的地理定位

从以 Android 7.0 为目标平台的应用开始，地理定位 API 将仅在安全的起点（通过 HTTPS）上被允许。此政策的目的是在用户使用不安全连接时保护他们的私人信息。

测试 WebView 测试版

WebViewis 定期更新，因此我们建议您经常使用 WebView 的测试版本测试应用的兼容性。要在 Android 7.0 上着手测试 WebView 的预发布版本，请下载并安装 Chrome Dev 或 Chrome 测试版，然后按上述说明在开发者选项下面选择它作为 WebView 实现。请通过 [Chromium 错误跟踪程序](https://bugs.chromium.org/p/chromium/issues/entry?template=Webview Bugs)报告问题，以便我们可以在发布新的 WebView 版本前修复问题。

OpenGL™ ES 3.2 API

Android 7.0 添加了框架接口和对 OpenGL ES 3.2 的平台支持，包括：

- 来自 [Android 扩展包](https://www.khronos.org/registry/gles/extensions/ANDROID/ANDROID_extension_pack_es31a.txt) (AEP) 的所有扩展（`EXT_texture_sRGB_decode` 除外）。 
- 针对 HDR 的浮点帧缓冲和延迟着色。 
- BaseVertex 绘图调用可实现更好的批处理和流媒体服务。 
- 强大的缓冲区访问控制可减少 WebGL 开销。

Android 7.0 上适用于 OpenGL ES 3.2 的框架 API 与 `GLES32` 类一起提供。使用 OpenGL ES 3.2 时，请务必通过 `` 标记和 `android:glEsVersion` 属性在您的清单文件中声明要求。 

如需了解有关使用 OpenGL ES 的信息，包括如何在运行时检查设备支持的 OpenGL ES 版本，请参阅 [OpenGL ES API 指南](https://developer.android.google.cn/guide/topics/graphics/opengl)。

Android TV 录制

Android 7.0 通过新的录制 API 添加了从 Android TV 输入服务录制和播放内容的功能。构建在现有时移 API 之上，TV 输入服务可以控制能够录制的渠道数据、保存录制的会话的方式，同时可通过录制的内容管理用户交互。 

如需了解详细信息，请参阅 [Android TV Recording API](https://developer.android.google.cn/preview/features/tv-recording-api)。

Android for Work

Android for Work 针对运行 Android 7.0 的设备添加了许多新功能和 API。部分重要内容如下— 有关变更的完整列表，请参阅 [Android for Work 更新](https://developer.android.google.cn/preview/features/afw)。

工作资料安全性挑战 

面向 N SDK 的配置文件所有者可以为在工作资料中运行的应用指定单独的安全性挑战。当用户尝试打开任何工作应用时将显示工作挑战。成功完成安全性挑战可解锁工作资料并将其解密（如果需要）。对于配置文件所有者，`ACTION_SET_NEW_PASSWORD` 提示用户设置工作挑战，`ACTION_SET_NEW_PARENT_PROFILE_PASSWORD` 提示用户设置设备锁。

配置文件所有者可以使用 `setPasswordQuality()`、`setPasswordMinimumLength()` 和相关方法针对工作挑战设置不同的密码策略（例如，PIN 码必须多长，或是否可以使用指纹解锁配置文件）。配置文件所有者还可以使用新的 `getParentProfileInstance()` 方法返回的 `DevicePolicyManager` 实例设置设备锁定。此外，配置文件所有者可以使用新的 `setOrganizationColor()` 和 `setOrganizationName()` 方法针对工作挑战自定义凭据屏幕。

关闭工作 

在有工作资料的设备上，用户可以切换工作模式。工作模式关闭时，管理的用户临时关闭，其停用托管工作资料应用、后台同步和通知。这包括配置文件所有者应用。关闭工作模式时，系统显示永久状态图标，以提醒用户他们无法启动工作应用。启动器指示该工作应用和小部件无法访问。 

Always on VPN 

设备所有者和配置文件所有者可以确保工作应用始终通过指定的 VPN 连接。系统在设备启动后自动启动该 VPN。

新的 `DevicePolicyManager` 方法为 `setAlwaysOnVpnPackage()` 和 `getAlwaysOnVpnPackage()`。

由于 VPN 服务无需应用交互即可由系统直接绑定，因此，VPN 客户端必须针对 Always on VPN 处理新的入口点。和以前一样，由与操作 `android.net.VpnService` 匹配的 intent 过滤器将服务指示给系统。 

用户还可以使用 **Settings>More>Vpn** 手动设置实现 `VPNService` 方法的 Always on VPN 客户端。通过“设置”启用 Always on VPN 的选项仅在 VPN 客户端以 API 级别 24 为目标时可用。

自定义配置

应用可以用企业颜色和徽标来自定义配置文件所有者和设备所有者配置流程。`DevicePolicyManager.EXTRA_PROVISIONING_MAIN_COLOR` 自定义流程颜色。`DevicePolicyManager.EXTRA_PROVISIONING_LOGO_URI` 用企业徽标自定义流程。

无障碍增强功能

Android 7.0 现在针对新的设备设置直接在欢迎屏幕上提供“Vision Settings”。这使用户可以更容易发现和配置他们设备上的无障碍功能，包括放大手势、字体大小、显示屏尺寸和话语提示。 

随着这些无障碍功能更为突出，在启用这些功能后，您的用户更可能试用您的应用。请务必提前启用这些设置测试您的应用。您可以通过 Settings > Accessibility 启用它们。

还是在 Android 7.0 中，无障碍服务现在可以帮助具有动作障碍的用户触摸屏幕。全新的 API 允许使用人脸追踪、眼球追踪、点扫描等功能构建服务，以满足这些用户的需求。

如需了解详细信息，请参阅可下载的 [API 参考](https://developer.android.google.cn/preview/setup-sdk#docs-dl)中的 `android.accessibilityservice.GestureDescription`。

直接启动

直接启动可以缩短设备启动时间，让注册的应用具有有限的功能，即使在意外重启后。例如，如果当用户睡觉时加密的设备重启，那么注册的警报、消息和来电现在可以和往常一样继续通知用户。这也意味着重启后无障碍服务会立即可用。

在 Android 7.0 中，直接启动充分利用基于文件的加密，以针对系统和应用数据启用细化的加密策略。系统针对选定的系统数据和显式注册的应用数据使用设备加密存储。默认情况下，凭据加密存储可用于所有其他系统数据、用户数据、应用及应用数据。 

启动时，系统在受限的模式中启动，仅访问设备加密数据，不会对应用或数据进行常规访问。如果您有想要在此模式下运行的组件，您可以通过在清单中设置标记注册它们。重启后，系统通过广播 `LOCKED_BOOT_COMPLETED` intent 激活注册的组件。系统确保注册的设备加密的应用数据在解锁前可用。所有其他数据在用户确认锁定屏幕凭据进行解密前均不可用。 

如需了解详细信息，请参阅[直接启动](https://developer.android.google.cn/preview/features/direct-boot)。





密钥认证

Android 7.0 引入*密钥认证*，这是一个新的安全工具，可帮助您确保设备的[*硬件支持的密钥库*](https://source.android.google.cn/security/keystore/)中存储的密钥对适当保护您的应用使用的敏感信息。借助此工具，您可以更加放心地让您的应用与驻留在安全硬件中的密钥交互，即使运行您的应用的设备已被破解 root 权限。如果您在应用中使用硬件支持的密钥库中的密钥，您应使用此工具，尤其当您使用密钥验证应用中的敏感信息时。

通过密钥认证，您可以在设备的可信执行环境 (TEE) 中验证在设备的硬件支持的密钥库中创建和存储的 RSA 或 EC 密钥对。通过此工具，您还可以使用设备服务，例如您的应用的后端服务器，确定和有效验证密钥对的使用和有效性。这些功能为保护密钥对提供额外的安全级别，即使有人破解设备的 root 权限或损害运行于设备的 Android 平台的安全。

**注：**仅少部分运行 Android 7.0 的设备支持硬件级密钥认证；其他所有运行 Android 7.0 的设备则使用软件级密钥认证。在生产级环境中验证设备的硬件支持的密钥之属性前，您应确保设备支持硬件级密钥认证。为此，您应确保认证证书链包含由 Google 认证根密钥签署的根证书，且[密钥说明](https://developer.android.google.cn/preview/features/key-attestation#certificate_schema_keydescription)数据结构中的 `attestationSecurityLevel` 元素设置为 TrustedEnvironment 安全级别。

如需了解详细信息，请参阅[密钥认证](https://developer.android.google.cn/preview/features/key-attestation)开发者文档。

网络安全性配置

在 Android 7.0 中，通过使用说明性*“网络安全性配置”*（而不是使用传统的易出错的编程 API（例如，X509TrustManager）），应用可以安全地自定义其安全（HTTPS、TLS）连接的行为，无需任何代码修改。

支持的功能：

- **自定义信任锚。**让应用可以针对安全连接自定义哪些证书颁发机构 (CA) 值得信赖。例如，信任特定的自签署证书或限制应用信任的公共 CA 集。
- **仅调试重写。**让应用开发者可以安全调试其应用的安全连接，而不会增加安装基础的风险。
- **明文流量选择退出。**让应用可以防止自身意外使用明文流量。
- **证书固定。**这是一项高级功能，让应用可以针对安全连接限制哪些服务器密钥受信任。

如需了解详细信息，请参阅[网络安全性配置](https://developer.android.google.cn/preview/features/security-config)。

默认受信任的证书颁发机构

默认情况下，面向 Android 7.0 的应用仅信任系统提供的证书，且不再信任用户添加的证书颁发机构 (CA)。如果面向 Android N 的应用希望信任用户添加的 CA，则应使用[网络安全性配置](https://developer.android.google.cn/preview/features/security-config)以指定信任用户 CA 的方式。

APK signature scheme v2

Android 7.0 引入一项新的应用签名方案 APK Signature Scheme v2，它能提供更快的应用安装时间和更多针对未授权 APK 文件更改的保护。在默认情况下，Android Studio 2.2 和 Android Plugin for Gradle 2.2 会使用 APK Signature Scheme v2 和传统签名方案来签署您的应用。

虽然我们建议您对您的应用采用 APK Signature Scheme v2，但这项新方案并非强制性的。如果您的应用在使用 APK Signature Scheme v2 时不能正确开发，您可以停用这项新方案。禁用过程会导致 Android Studio 2.2 和 Android Plugin for Gradle 2.2 仅使用传统签名方案来签署您的应用。要仅用传统方案签署，打开模块级 `build.gradle` 文件，然后将行 `v2SigningEnabled false` 添加到您的版本签名配置中：

```
  android {
    ...
    defaultConfig { ... }
    signingConfigs {
      release {
        storeFile file("myreleasekey.keystore")
        storePassword "password"
        keyAlias "MyReleaseKey"
        keyPassword "password"
        v2SigningEnabled false
      }
    }
  }
```

**注意：**如果您使用 APK Signature Scheme v2 签署您的应用，并对应用进行了进一步更改，则应用的签名将无效。出于这个原因，请在使用 APK Signature Scheme v2 签署您的应用之前、而非之后使用 `zipalign` 等工具。

如需了解详细信息，请阅读相关的 Android Studio 文档，这些文档介绍了如何在 Android Studio 中[签署应用](https://developer.android.google.cn/studio/publish/app-signing#release-mode)以及如何使用 Android Plugin for Gradle [为签署应用配置构建文件](https://developer.android.google.cn/studio/build/build-variants#signing)。

作用域目录访问

在 Android 7.0 中，应用可以使用新的 API 请求访问特定的[外部存储](https://developer.android.google.cn/guide/topics/data/data-storage#filesExternal)目录，包括可移动媒体上的目录，如 SD 卡。新 API 大大简化了应用访问标准外部存储目录的方式，如 `Pictures` 目录。应用（如照片应用）可以使用这些 API（而不是使用 `READ_EXTERNAL_STORAGE`），其授予所有存储目录的访问权限或存储访问框架，从而让用户可以导航到目录。

此外，新的 API 简化了用户向应用授予外部存储访问权限的步骤。当您使用新的 API 时，系统使用一个简单的权限 UI，其清楚地详细介绍应用正在请求访问的目录。

如需了解详细信息，请参阅[作用域目录访问](https://developer.android.google.cn/preview/features/scoped-folder-access)开发者文档。

键盘快捷键辅助工具

在 Android 7.0 中，用户可以按**“Meta + /”**触发*“键盘快捷键”*屏幕，它会显示的系统和对焦的应用中可用的所有快捷键。如果快捷键存在，系统自动从应用菜单检索这些快捷键。您也可以为屏幕提供微调的快捷键列表。您可以通过重写新 `Activity.onProvideKeyboardShortcuts()` 的方法来进行这项操作，如可下载的 [API 参考](https://developer.android.google.cn/preview/setup-sdk#docs-dl)中所述。

**注**：所有键盘都没有 **Meta** 键：在 Macintosh 键盘上，它是 **Command** 键；在 Windows 键盘上，它是 **Windows** 键；而在 Pixel C 和 Chrome 操作系统键盘上，它是 **Search** 键。

要在您的应用的任何地方触发键盘快捷键辅助工具，为相关 Activity 调用 `Activity.requestKeyboardShortcutsHelper()`。

Custom Pointer API

Android 7.0 引入 Custom Pointer API，以便您可以自定义指针的外观、 可见性和行为。此功能在用户使用鼠标或触控板与 UI 对象交互尤为有用。默认指针使用标准图标。此 API 还包含多种高级功能，例如根据鼠标或触控板特定移动情况改变指针图标外观。

要设置指针图标，请替换 `View` 类的 `onResolvePointerIcon()` 方法。此方法使用 `PointerIcon` 对象绘制与特定移动事件对应的图标。

Sustained Performance API

长期运行的应用的性能可能会显著波动，因为系统会阻止系统芯片在设备组件达到温度限制时启动。这种波动是建立高性能长期运行应用的应用开发者的移动目标。

为解决这些限制，Android 7.0 包括了对*持续性能模式*的支持，帮助原始设备制造商 (OEM) 提供关于长期运行应用的设备性能能力的提示。应用开发者可以使用这些提示来根据可预测的一致设备性能水平调整长期应用。

应用开发者只能在 Nexus 6P 设备的 Android 7.0 中尝试这款新 API。要使用此功能，为您希望以持续性能模式运行的窗口设置持续性能窗口标记。使用 `Window.setSustainedPerformanceMode()` 方法设置此标记。当窗口不再对焦时，系统会自动停用此模式。

VR 支持

Android 7.0 添加了新的 VR 模式的平台支持和优化，以使开发者能为用户打造高质量移动 VR 体验。增加了一些性能增强特性，包括允许 VR 应用访问某个专属的 CPU 核心。在您的应用中，您可以充分利用到专为 VR 设计的智能头部跟踪和立体声通知功能。最重要的是，Android 7.0 的图形延时非常低。如需了解有关开发面向 Android 7.0 的 VR 应用的完整信息，请参阅[面向 Android 的 Google VR SDK](https://developers.google.cn/vr/android/)。

打印服务增强

在 Android 7.0 中，打印服务开发者现在可以公开关于个别打印机和打印作业的其他信息。

在列出各打印机时，打印服务现在可以通过两种方式来设置按打印机的图标：

- 您可以通过调用 `PrinterInfo.Builder.setResourceIconId()` 设置源于资源 ID 的图标
- 您可以通过调用 `PrinterInfo.Builder.setHasCustomPrinterIcon()`，并针对使用 `android.printservice.PrinterDiscoverySession.onRequestCustomPrinterIcon()` 请求图标的情况设置回调来显示源自网络的图标

此外，您还可以通过调用 `PrinterInfo.Builder.setInfoIntent()` 提供按打印机活动，以显示其他信息。

您可以通过分别调用 `android.printservice.PrintJob.setProgress()` 和 `android.printservice.PrintJob.setStatus()` 在打印任务通知中指示打印任务的进度和状态。

如需了解有关这些方法的详细信息，请参阅可下载的 [API 参考](https://developer.android.google.cn/preview/setup-sdk#docs-dl)。

FrameMetricsListener API

FrameMetricsListener API 允许应用监测它的 UI 渲染性能。API 通过公开流式传输 Pub/Sub API 来提供此能力，以传递应用当前窗口的帧计时信息。返回的数据相当于 `adb shell dumpsys gfxinfo framestats` 显示的数据，但不限定于在过去的 120 帧内。

您可以使用 FrameMetricsListener 来衡量生产中的交互级 UI 性能，无需 USB 连接。此 API 允许在比 `adb shell dumpsys gfxinfo` 更高的粒度上收集数据。因为系统可以从应用中的特定交互中收集数据，因此更高的粒度变得可行；系统不需要采集关于完整应用性能的全局概要或清除任何全局状态。您可以使用这种能力来针对应用的真实使用案例收集性能数据和捕捉 UI 性能回归。

要监测一个窗口，实现 `FrameMetricsListener.onMetricsAvailable()` 回调方法，并在窗口上注册。如需了解详细信息，请参阅可下载的 [API 参考](https://developer.android.google.cn/preview/setup-sdk#docs-dl)中的 `FrameMetricsListener` 类文档。

API 提供了一个包含计时数据的 `FrameMetrics` 对象，其渲染子系统会在一帧长度内报告各种里程碑。支持的指标有：`UNKNOWN_DELAY_DURATION`、`INPUT_HANDLING_DURATION`、`ANIMATION_DURATION`、`LAYOUT_MEASURE_DURATION`、`DRAW_DURATION`、 `SYNC_DURATION`、`COMMAND_ISSUE_DURATION`、`SWAP_BUFFERS_DURATION`、`TOTAL_DURATION` 和 `FIRST_DRAW_FRAME`。

虚拟文件

在较早的 Android 版本中，您的应用可以使用存储访问框架来允许用户从他们的云存储帐户中选择文件，如 Google Drive。但是，不能表示没有直接字节码表示的文件；每个文件都必须提供一个输入流。

Android 7.0 在存储访问框架中添加了*虚拟文件*的概念。虚拟文件功能可以让您的 `DocumentsProvider` 返回可与 `ACTION_VIEW` intent 使用的文件 URI，即使它们没有直接字节码表示。Android 7.0 还允许您为用户文件（虚拟或其他类）提供备用格式。

为获得您的应用中的虚拟文件的 URI，首先您应创建一个 `Intent` 以打开文件选择器 UI。由于应用不能使用 `openInputStream()` 方法来直接打开一个虚拟文件，因此如果您包括了 `CATEGORY_OPENABLE` 类别，您的应用不会收到任何虚拟文件。

在用户选择之后，系统调用 `onActivityResult()` 方法。您的应用可以检索虚拟文件的 URI，并得到一个输入流，这表现在以下片段中的代码。

```
 // Other Activity code ... final static private int REQUEST_CODE = 64; // We listen to the OnActivityResult event to respond to the user's selection. @Override public void onActivityResult(int requestCode, int resultCode,  Intent resultData) {   try {    if (requestCode == REQUEST_CODE &&      resultCode == Activity.RESULT_OK) {      Uri uri = null;      if (resultData != null) {        uri = resultData.getData();        ContentResolver resolver = getContentResolver();        // Before attempting to coerce a file into a MIME type,        // check to see what alternative MIME types are available to        // coerce this file into.        String[] streamTypes =         resolver.getStreamTypes(uri, "*/*");        AssetFileDescriptor descriptor =          resolver.openTypedAssetFileDescriptor(            uri,            streamTypes[0],            null);        // Retrieve a stream to the virtual file.        InputStream inputStream = descriptor.createInputStream();      }    }   } catch (Exception ex) {    Log.e("EXCEPTION", "ERROR: ", ex);   } }
```