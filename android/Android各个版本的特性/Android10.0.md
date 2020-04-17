# Android 10.0新特性

### [官网Android 10.0新特性](https://developer.android.google.cn/about/versions/10/highlights)

可折叠设备

Android 10 基于强大的多窗口支持构建而成，扩展了跨应用窗口的多任务处理能力，还提供了屏幕连续性，可以在设备折叠或展开时维持应用状态。Android 10 在 [onResume](https://developer.android.google.cn/reference/android/app/Activity.html#onResume()) 和 [onPause](https://developer.android.google.cn/reference/android/app/Activity.html#onPause()) 中添加了多项改进，用于支持多项恢复，并在应用获得焦点时通知应用。它还更改了 [resizeableActivity](https://developer.android.google.cn/guide/topics/ui/multi-window#resizeableActivity) 清单属性的工作方式，以帮助您管理应用在可折叠设备和大屏幕设备上的显示方式。为帮助针对可折叠设备进行编译，您可以在 Android Studio 中配置可折叠模拟器来用作虚拟设备 (AVD)。如需详细了解如何针对可折叠设备优化应用，请参阅[开发者指南](https://developer.android.google.cn/guide/topics/ui/foldables)。

5G 网络

5G 有望在稳定提升速度的同时降低延迟，Android 10 新增了针对 5G 的平台支持，并扩展了[现有 API](https://developer.android.google.cn/reference/android/net/ConnectivityManager) 来帮助您充分利用这些增强功能。您可以使用连接 API 来检测设备是否具有高带宽连接，还可以检查连接是否按流量计费。借助这些功能，您的应用和游戏可以为使用 5G 的用户量身打造丰富的沉浸式体验。

通知中的智能回复

Android 10 使用设备上的机器学习在通知中提供上下文操作建议，如智能回复消息或在通知中打开某个地址的地图。您的应用可以立即充分利用此功能，而您无需执行任何操作。系统提供的智能回复和操作默认直接插入到通知中。您仍可以根据需要自行提供回复或操作。使用 [setAllowGeneratedReplies()](https://developer.android.google.cn/reference/android/app/Notification.Action.Builder#setAllowGeneratedReplies(boolean)) 和 [setAllowSystemGeneratedContextualActions()](https://developer.android.google.cn/reference/android/app/Notification.Builder#setAllowSystemGeneatedContextualActions(boolean)) 即可针对每则通知选择停用智能回复。

![img](https://developer.android.google.cn/images/about/versions/10/overview/image10.png)

*智能回复可以根据通知内容提供操作建议。*

深色主题

Android 10 新增了一个系统级的深色主题，非常适合光线较暗的场景并能帮助节省电量。用户转至“设置”进行相应设置或开启“省电模式”即可激活新的系统级深色主题。这会将系统界面更改为深色，并为支持深色主题的应用启用深色主题。您可以为应用构建自定义深色主题，也可以选择使用新的 Force Dark 功能，让系统根据现有主题动态创建深色版本。您还可以充分利用 [AppCompat 的 DayNight 功能](https://developer.android.google.cn/preview/features/darktheme)，为使用早期版本的 Android 的用户提供深色主题。如需了解详情，请参阅[开发者指南](https://developer.android.google.cn/guide/topics/ui/look-and-feel/darktheme)。

![img](https://developer.android.google.cn/images/about/versions/10/overview/image12.png)

*Android 10 可以利用 Force Dark 为应用动态创建深色主题。*

手势导航

![img](https://developer.android.google.cn/images/about/versions/10/overview/gesture.gif)

*手势导航可让应用全屏显示内容。*

Android 10 引入了全手势导航模式，该模式不显示通知栏区域，允许应用使用全屏来提供更丰富、更让人沉浸的体验。它通过边缘滑动（而不是可见的按钮）保留了用户熟悉的“返回”、“主屏幕”和“最近”导航。要与手势导航无缝融合，您应顺着边缘在导航栏后方绘制，以打造沉浸式体验。要实现这一点，应用应使用 [setSystemUiVisibility()](https://developer.android.google.cn/reference/android/view/View.html#setSystemUiVisibility(int)) API 以全屏模式布局，然后相应地处理 [WindowInsets](https://developer.android.google.cn/reference/android/view/WindowInsets)，以确保重要的界面区域未被遮挡。立即[开始优化您的应用](https://developer.android.google.cn/guide/navigation/gesturenav)，并查看我们的[博文系列](https://medium.com/androiddevelopers/gesture-navigation-going-edge-to-edge-812f62e4e83e)，以了解详情。

设置面板

现在，您可以通过新的[设置面板 API](https://developer.android.google.cn/reference/android/provider/Settings.Panel) 在应用上下文中直接显示关键系统设置。设置面板是浮动界面，您可以通过调用它来显示用户可能需要使用的设置，如互联网连接、NFC 和音量。例如，浏览器可以显示具有飞行模式、WLAN（包括附近网络）和移动数据等连接设置的面板。要显示设置面板，只需发出具有某个新 [Settings.Panel 操作](https://developer.android.google.cn/reference/android/provider/Settings.Panel.html#ACTION_INTERNET_CONNECTIVITY)的 intent。

共享快捷方式

共享快捷方式功能可使共享更加轻松快捷，让用户能够直接跳转到其他应用来共享内容。开发者可以发布能在应用中启动特定 Activity 的共享目标，同时附上内容；这些共享目标会在共享界面中向用户显示。因为共享目标是提前发布的，所以共享界面会在启动后立即加载它们。共享快捷方式类似于应用快捷方式，都使用同一个 [ShortcutInfo API](https://developer.android.google.cn/reference/android/content/pm/ShortcutInfo)。ShareTarget AndroidX 库也支持此 API。如需了解详情，请参阅[示例应用](https://github.com/googlesamples/android-SharingShortcuts)。

![img](https://developer.android.google.cn/images/about/versions/10/overview/image11.png)

*共享快捷方式可让用户直接跳转到应用中的特定 Activity，同时附上内容。*

用户隐私设置

隐私权是 Android 10 的其中一个主要关注点，相关改进包括在平台中提供更强大的保护措施以及在设计新功能时谨记隐私性。Android 10 基于先前版本构建，并引入了大量变更（如改进了系统界面、让权限授予更加严格以及对应用能够使用哪些数据实施了限制），目的是保护隐私权并赋予用户更多控制权。如需详细了解如何在您的应用中支持这些变更，请参阅[隐私权变更](https://developer.android.google.cn/about/versions/10/privacy/changes)。

![img](https://developer.android.google.cn/images/about/versions/10/overview/location.png)

*用户现在可以选择在应用在前台运行时授予其访问位置信息的权限。*

**赋予用户对位置数据的更多控制权** - 用户可以通过新的权限选项更好地控制他们的位置数据；现在，他们可以允许应用仅在实际使用（在前台运行）时访问位置信息。对于大部分应用来说，这提供了足够的访问级别；而对于用户来说，这在确保透明度和控制权方面是一项重大改进。要详细了解位置信息方面的变更，请参阅[开发者指南](https://developer.android.google.cn/training/location/receive-location-updates)或我们的[博文](https://android-developers.googleblog.com/2019/03/giving-users-more-control-over-their.html)。

**在扫描网络时保护位置数据** - 用于扫描网络的大多数 API 都需要粗略位置权限。Android 10 [改为要求精确位置权限](https://developer.android.google.cn/about/versions/10/privacy/changes#location-telephony-wifi-bluetooth)，由此来增强对这些 API 的防御。

**阻止设备跟踪** - 应用无法再访问不可重置的设备标识符（可用于跟踪），包括设备 IMEI、序列号和类似标识符。设备的 MAC 地址也会默认在连接到 WLAN 网络时随机分配。请阅读[最佳做法](https://developer.android.google.cn/training/articles/user-data-ids)，其中的内容有助于您为具体使用场景选择合适的标识符；同时点击[此处](https://developer.android.google.cn/preview/privacy/data-identifiers)了解详情。

**保护外部存储设备中的用户数据** - Android 10 引入了一些变更，目的是让用户更好地控制外部存储设备中的文件以及其中的应用数据。应用可以将自己的文件存储在专用沙盒中，但必须使用 MediaStore 来访问共享媒体文件，并使用系统文件选择器访问新的“下载内容”集合中的共享文件。如需了解详情，请点击[此处](https://developer.android.google.cn/about/versions/10/privacy/changes#scoped-storage)。

**屏蔽意外中断** - Android 10 可阻止应用从后台启动，从后台启动会使应用意外跳转到前台并从其他应用获得焦点。如需了解详情，请点击[此处](https://developer.android.google.cn/about/versions/10/privacy/changes#background-activity-starts)。

安全性

Android 10 引入了[多项功能](https://security.googleblog.com/2019/05/whats-new-in-android-q-security.html)，可通过加密、平台安全强化和身份验证方面的改进为用户提供更高的安全性。请详细阅读[此处的 Android 10 安全更新](https://android-developers.googleblog.com/2019/05/whats-new-in-android-q-security.html)。

**存储加密** - 搭载 Android 10 的所有兼容设备都必须加密用户数据；为了提高加密效率，Android 10 引入了我们的新加密模式 [Adiantum](https://source.android.google.cn/security/encryption/adiantum)。

**默认启用 TLS 1.3** - Android 10 还默认启用 [TLS 1.3](https://www.ietf.org/blog/tls13/)，它是 TLS 标准的主要修订版本，具有性能优势和[更高的安全性](https://developer.android.google.cn/about/versions/10/behavior-changes-all#tls-1.3)。

**平台安全强化** - Android 10 还引入了[针对平台几个关键安全区域的安全强化](https://security.googleblog.com/2019/05/queue-hardening-enhancements.html)功能。

**改进了生物识别功能** - Android 10 扩展了 [BiometricPrompt](https://developer.android.google.cn/reference/android/hardware/biometrics/package-summary) 框架，以支持被动身份验证方法，如人脸识别以及添加隐式和显式身份验证流程。在显式流程中，用户必须在身份验证期间明确确认 TEE 中的事务。对于需要被动身份验证的事务，隐式流程是一种更轻量的替代方案。Android 10 还改进了按需回退设备凭据的流程。如需了解详情，请点击[此处](https://developer.android.google.cn/training/sign-in/biometric-auth)。

摄像头和媒体

照片的动态深度

应用现在可以请求动态深度图片，其中包含与深度相关元素有关的 JPEG、XMP 元数据，以及嵌入在同一文件中的深度和置信度映射。这些功能让您可以在应用中提供专用模糊和散景选项。动态深度是用于生态系统的一种[开源格式](https://developer.android.google.cn/training/camerax/Dynamic-depth-v1.0.pdf)，我们正在与合作伙伴合作，以将其推广到搭载 Android 10 及更高版本的设备。

![img](https://developer.android.google.cn/images/about/versions/10/overview/depthtrue.jpg)

![img](https://developer.android.google.cn/images/about/versions/10/overview/depthblur.jpg)

![img](https://developer.android.google.cn/images/about/versions/10/overview/depthmap.jpg)

*您可以利用动态深度图片在应用中提供专用模糊和散景选项。*

捕获播放的音频

现在，播放音频的任何应用都允许其他应用使用[新的音频播放捕获 API](https://developer.android.google.cn/guide/topics/media/playback-capture) 捕获其音频流。除了能够启用字幕之外，此 API 还可让您支持常见的使用场景（如直播游戏）。我们在构建这项新功能时考虑了隐私性和版权保护，因此，应用捕获其他应用音频的功能会受限，这会让应用全权控制其音频流是否可以被捕获。如需了解详情，请阅读这篇[博文](https://android-developers.googleblog.com/2019/07/capturing-audio-in-android-q.html)。

新的音频和视频编解码器

Android 10 新增了对开源视频编解码器 [AV1](https://en.wikipedia.org/wiki/AV1) 的支持，这允许媒体提供商[使用更少的带宽](https://en.wikipedia.org/wiki/AV1#Quality_and_efficiency)向 Android 设备流式传输高品质视频内容。此外，Android 10 还支持使用 [Opus](http://opus-codec.org/)（一种针对语音和音乐流式传输进行了优化的开放且免版税的编解码器）和 [HDR10+](https://en.wikipedia.org/wiki/High-dynamic-range_video#HDR10+)（用于支持它的设备上的高动态范围视频）对音频进行编码。[MediaCodecInfo API](https://developer.android.google.cn/reference/android/media/MediaCodecInfo) 引入了一种更简便的方法来确定某个 Android 设备的视频渲染功能。对于任何指定的编解码器，您可以获取其支持的大小和帧速率列表。

原生 MIDI API

针对使用 C++ 执行其音频处理的应用，Android 10 引入了[原生 MIDI API](https://developer.android.google.cn/ndk/guides/audio/midi)，以通过 NDK 与 MIDI 设备通信。此 API 允许使用非阻塞读取在音频回调内检索 MIDI 数据，从而以低延迟处理 MIDI 消息。使用示例应用和[此处的源代码](http://github.com/googlesamples/android-ndk/tree/master/native-midi)试试看。

可缩放的定向麦克风

Android 10 可让您通过新的 [MicrophoneDirection](https://developer.android.google.cn/reference/android/media/MicrophoneDirection) API 更好地控制音频捕获。您可以使用此 API 指定在录音时麦克风的首选方向。例如，当用户在进行视频“自拍”时，您可以[请求前置麦克风](https://developer.android.google.cn/reference/android/media/MicrophoneDire ction#setMicrophoneDirection(int))（如果有）以进行录音。此外，此 API 还引入了控制可缩放麦克风的标准化方法，允许您的应用控制[录音字段大小](https://developer.android.google.cn/reference/android/media/MicrophoneDirection#setMicrophoneFieldDimension(float))。

Vulkan 无处不在

Android 10 包含用于绘制高性能 3D 图形的低开销、跨平台 API [实现](https://developer.android.google.cn/ndk/guides/graphics/)，扩大了 [Vulkan](https://www.khronos.org/vulkan/) 的影响范围。所有搭载 Android 10 及更高版本的 64 位设备现在都要求使用 Vulkan 1.1，也建议在所有 32 位设备上使用 Vulkan 1.1。我们已经看到整个生态系统大力支持 Vulkan 的强劲势头，在搭载 Android N 或更高版本的设备中，53% 的设备都支持 Vulkan 1.0.3 或更高版本。随着 Android 10 中相关新要求的推出，我们预计未来一年 Vulkan 的采用率将进一步提升。

连接性

改进了点对点连接和互联网连接

我们重构了 WLAN 堆栈，目的是改进隐私设置和性能，同时改进常见使用场景（如管理 IoT 设备以及提供互联网连接建议），而无需请求位置权限。[网络连接 API](https://developer.android.google.cn/guide/topics/connectivity/wifi-bootstrap) 针对点对点功能（如配置、下载或打印）简化了通过本地 WLAN 管理 IoT 设备的操作。[网络建议 API](https://developer.android.google.cn/guide/topics/connectivity/wifi-suggest) 可让应用向用户显示首选 WLAN 网络以进行互联网连接。

WLAN 性能模式

应用现在可以通过启用[高性能和低延迟模式](https://developer.android.google.cn/reference/android/net/wifi/WifiManager.html#createWifiLock(int, java.lang.String))来请求自适应 WLAN。如果低延迟对用户体验（如实时游戏、活跃语音通话以及类似使用场景）至关重要，这些模式会极具优势。平台与设备固件配合使用，可以满足最低耗电量的要求。要使用新的性能模式，请调用 [WifiManager.WifiLock.createWifiLock()](https://developer.android.google.cn/reference/android/net/wifi/WifiManager.html#createWifiLock(int, java.lang.String))（使用 `WIFI_MODE_FULL_LOW_LATENCY` 或 `WIFI_MODE_FULL_HIGH_PERF`）。在这些模式中，平台与设备固件配合使用，可以满足最低耗电量的要求。

Android 基础知识

ART 优化

在 ART 运行时方面的改进可帮助您的应用更快地启动、占用更少的内存并更顺畅地运行，而您无需执行任何操作。借助 Google Play 提供的 [ART 配置文件](https://android-developers.googleblog.com/2019/04/improving-app-performance-with-art.html)，ART 在应用运行之前就可以预先编译应用组件。在运行时，Android 10 向 ART 的并发复制 (CC) 垃圾回收器添加了分代垃圾回收功能，以节省垃圾回收的时间并提高 CPU 效率，减少卡顿，同时帮助应用在低端设备上更顺畅地运行。

![img](https://developer.android.google.cn/images/about/versions/10/overview/art-profiles.png)

*上图以百分比形式显示了具体应用在使用 Play 配置文件进行测试后启动时间的缩短幅度。*

Neural Networks API 1.2

我们新增了 60 项操作（包括 ARGMAX、ARGMIN 和量化 LSTM），并进行了一系列性能优化。这为加速更多模型奠定了基础，比如对象检测模型和图像分割模型。我们与硬件供应商合作，并使用常见的机器学习框架（如 [TensorFlow](https://tensorflow.google.cn/)），以针对 NNAPI 1.2 进行优化并提供支持。

Thermal API

当设备过热时，它们可能会限制 CPU 和/或 GPU，而这可能会以意想不到的方式影响应用和游戏。现在，在 Android 10 中，应用和游戏可以使用 [Thermal API](https://developer.android.google.cn/reference/android/os/PowerManager#addThermalStatusListener(android.os.PowerManager.OnThermalStatusChangedListener)) 监控设备变化情况，并在设备过热时采取措施，使设备恢复到正常温度。例如，影音在线播放应用可以降低分辨率/比特率或减少网络流量；相机应用可以停用闪光灯或密集型图像增强；游戏可以降低帧速率或减少多边形曲面细分。如需了解详情，请点击[此处](https://developer.android.google.cn/about/versions/10/features#thermal)。

通过公共 API 实现兼容性

Android 10 继续增加了对非 SDK 接口的限制，以便应用逐步转为[仅使用公共 API](https://developer.android.google.cn/distribute/best-practices/develop/restrictions-non-sdk-interfaces)。如果您目前使用的接口受到限制，则可以选择[针对该接口请求新的公共 API](https://developer.android.google.cn/distribute/best-practices/develop/restrictions-non-sdk-interfaces#feature-request)。为了帮助您完成过渡并防止应用中断，我们仅在您的应用以 Android 10 (API 29) 为目标平台时实施这些限制。如需详细了解这些限制，请参阅[开发者指南](https://developer.android.google.cn/about/versions/10/non-sdk-q)。

更新速度更快，代码更新频率更高

Android 10 可通过 [Treble 计划](https://source.android.google.cn/devices/architecture)加快更新速度，这可在 Android 与设备制造商和芯片制造商提供的底层设备代码之间提供一致的可测试接口。借助 Treble 计划，设备制造商能够以更快的速度和更低的费用将 Android 10 引入符合 Treble 标准的设备中。

Android 10 也是首个支持 [Project Mainline](https://android-developers.googleblog.com/2019/05/fresher-os-with-projects-treble-and-mainline.html)（官方名称为“Google Play 系统更新”）的版本；这是我们用于保护 Android 用户并通过重要的代码变更及时更新设备的新技术，可通过 Google Play 直接获取。借助 Google Play 系统更新，我们能够更新所有搭载 Android 10 及更高版本的设备中的特定内部组件，无需设备制造商全面更新系统。

对于开发者来说，我们希望 Android 10 中的这些更新能够广泛帮助提升设备间平台实现的一致性，并随时间提供更高的统一性，从而降低您的开发和测试费用。