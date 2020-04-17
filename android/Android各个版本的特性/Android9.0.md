# Android 9.0新特性

### [官网Android 9.0新特性](https://developer.android.google.cn/about/versions/pie/android-9.0)

利用 Wi-Fi RTT 进行室内定位

![全新 RTT API 支持在应用中进行室内定位。](https://developer.android.google.cn/preview/images/rtt-nav.png)

Android 9 添加了对 IEEE 802.11mc Wi-Fi 协议（也称为 *Wi-Fi Round-Trip-Time* (RTT)）的平台支持，从而让您的应用可以利用室内定位功能。

在运行 Android 9 且具有硬件支持的设备上，应用可以使用 [RTT API](https://developer.android.google.cn/reference/android/net/wifi/rtt/package-summary) 来测量与附近支持 RTT 的 Wi-Fi *接入点* (AP) 的距离。 设备必须已启用位置服务并开启 Wi-Fi 扫描（在 **Settings > Location** 下），同时您的应用必须具有 [`ACCESS_FINE_LOCATION`](https://developer.android.google.cn/reference/android/Manifest.permission#ACCESS_FINE_LOCATION) 权限。

设备无需连接到接入点即可使用 RTT。 为了保护隐私，只有手机可以确定与接入点的距离；接入点无此信息。

如果您的设备测量与 3 个或更多接入点的距离，您可以使用一个多点定位算法来预估与这些测量值最相符的设备位置。 结果通常精准至 1 至 2 米。

通过这种精确性，您可以打造新的体验，例如楼内导航、基于精细位置的服务，如无歧义语音控制（例如，*“打开这盏灯”*），以及基于位置的信息（如 *“此产品是否有特别优惠？”*）。

显示屏缺口支持

![显示各种屏幕缺口尺寸的开发者选项界面](https://developer.android.google.cn/preview/images/emulator-devoptions-cutout_2x.png)

通过使用模拟器测试屏幕缺口。

Android 9 支持最新的全面屏，其中包含为摄像头和扬声器预留空间的屏幕缺口。 通过 [`DisplayCutout`](https://developer.android.google.cn/reference/android/view/DisplayCutout) 类可确定非功能区域的位置和形状，这些区域不应显示内容。 要确定这些屏幕缺口区域是否存在及其位置，请使用 [`getDisplayCutout()`](https://developer.android.google.cn/reference/android/view/WindowInsets#getDisplayCutout()) 函数。

全新的窗口布局属性 [`layoutInDisplayCutoutMode`](https://developer.android.google.cn/reference/android/view/WindowManager.LayoutParams#layoutInDisplayCutoutMode) 让您的应用可以为设备屏幕缺口周围的内容进行布局。 您可以将此属性设为下列值之一：

- [`LAYOUT_IN_DISPLAY_CUTOUT_MODE_DEFAULT`](https://developer.android.google.cn/reference/android/view/WindowManager.LayoutParams#LAYOUT_IN_DISPLAY_CUTOUT_MODE_DEFAULT)
- [`LAYOUT_IN_DISPLAY_CUTOUT_MODE_SHORT_EDGES`](https://developer.android.google.cn/reference/android/view/WindowManager.LayoutParams#LAYOUT_IN_DISPLAY_CUTOUT_MODE_SHORT_EDGES)
- [`LAYOUT_IN_DISPLAY_CUTOUT_MODE_NEVER`](https://developer.android.google.cn/reference/android/view/WindowManager.LayoutParams#LAYOUT_IN_DISPLAY_CUTOUT_MODE_NEVER)

可以按以下方法在任何运行 Android 9 的设备或模拟器上模拟屏幕缺口：

1. 启用[开发者选项](https://developer.android.google.cn/studio/debug/dev-options)。
2. 在 **Developer options** 屏幕中，向下滚动至 **Drawing** 部分并选择 **Simulate a display with a cutout**。
3. 选择屏幕缺口的大小。

注：我们建议您通过使用运行 Android 9 的设备或模拟器测试屏幕缺口周围的内容显示。

通知

Android 9 引入了多个通知增强功能，可供以 API 级别 28 及以上版本作为目标平台的开发者使用。

![短信通知](https://developer.android.google.cn/preview/images/p-messaging.jpg)

附带了照片的 MessagingStyle。

![短信通知](https://developer.android.google.cn/preview/images/p-replies.jpg)

含回复和对话的 MessagingStyle。

提升短信体验

从 Android 7.0（API 级别 24）开始，您可以添加一个操作以回复短信或直接从通知中输入其他文本。 Android 9 通过下列增强提升了该功能：

- 简化了针对对话参与者的支持：[`Person`](https://developer.android.google.cn/reference/android/app/Person) 类可用于识别参与对话的人员，包括他们的头像和 URI。 现在，许多其他 API（如 [`addMessage()`](https://developer.android.google.cn/reference/android/app/Notification.MessagingStyle#addMessage(java.lang.CharSequence, long, android.app.Person))）均可利用 [`Person`] 类而不是 `CharSequence`。 `Person` 类也支持构建器设计模式。
- 支持图像：现在，Android 9 可在手机的“短信通知”中显示图像。 您可以使用对短信使用 [`setData()`](https://developer.android.google.cn/reference/android/app/Notification.MessagingStyle.Message#setData(java.lang.String, android.net.Uri))来显示图像。 以下代码段演示了如何创建 `Person` 和包含图像的短信。



[KOTLIN](https://developer.android.google.cn/about/versions/pie/android-9.0#kotlin)

[JAVA](https://developer.android.google.cn/about/versions/pie/android-9.0#java)

```kotlin
// Create new Person.
val sender = Person()
        .setName(name)
        .setUri(uri)
        .setIcon(null)
        .build()
// Create image message.
val message = Message("Picture", time, sender)
        .setData("image/", imageUri)
val style = Notification.MessagingStyle(getUser())
        .addMessage("Check this out!", 0, sender)
        .addMessage(message)
```







- 将回复另存为草稿：当用户无意中关闭一个短信通知时，您的应用可以检索系统发送的 [`EXTRA_REMOTE_INPUT_DRAFT`](https://developer.android.google.cn/reference/android/app/Notification#EXTRA_REMOTE_INPUT_DRAFT)。 您可以使用此 extra 预填充应用中的文本字段，以便用户可以完成他们的回复。
- 确定对话是否为群组对话。您可以使用 [`setGroupConversation()`](https://developer.android.google.cn/reference/android/app/Notification.MessagingStyle#setGroupConversation(boolean)) 以明确确定对话是否为群组对话。
- 为 Intent 设置语义操作：[`setSemanticAction()`](https://developer.android.google.cn/reference/android/app/Notification.Action.Builder#setSemanticAction(int)) 函数允许您为操作提供语义含义，如“标记为已读”、“删除”和“回复”等。
- SmartReply：Android 9 支持在您的短信应用中提供相同的建议回复。 使用 [`RemoteInput.setChoices()`](https://developer.android.google.cn/reference/android/app/RemoteInput.Builder#setChoices(java.lang.CharSequence[])) 为用户提供一组标准回复。

渠道设置、广播和请勿打扰

Android 8.0 引入了[通知渠道](https://developer.android.google.cn/guide/topics/ui/notifiers/notifications#ManageChannels)，允许您为要显示的每种通知类型创建可由用户自定义的渠道。 Android 9 通过下列变更简化通知渠道设置：

- 屏蔽渠道组：现在，用户可以针对某个应用在通知设置中屏蔽整个渠道组。 您可以使用 [`isBlocked()`](https://developer.android.google.cn/reference/android/app/NotificationChannelGroup#isBlocked()) 函数确定何时屏蔽一个渠道组，从而不会向该组中的渠道发送任何通知。

  此外，您的应用可以使用全新的 [`getNotificationChannelGroup()`](https://developer.android.google.cn/reference/android/app/NotificationManager#getNotificationChannelGroup(java.lang.String)) 函数查询当前渠道组设置。

- 全新的广播 Intent 类型：现在，当通知渠道和渠道组的屏蔽状态发生变更时，Android 系统将发送广播 Intent。 拥有已屏蔽的渠道或渠道组的应用可以侦听这些 Intent 并做出相应的回应。 有关这些 Intent 操作和 extra 的更多信息，请参阅 [`NotificationManager`](https://developer.android.google.cn/reference/android/app/NotificationManager#constants) 参考中更新的常量列表。 有关响应广播 Intent 的信息，请参阅[广播](https://developer.android.google.cn/guide/components/broadcasts.html)。

- [`NotificationManager.Policy`](https://developer.android.google.cn/reference/android/app/NotificationManager.Policy#constants) 有 3 种新的“请勿打扰”优先级类别：

  - [`PRIORITY_CATEGORY_ALARMS`](https://developer.android.google.cn/reference/android/app/NotificationManager.Policy#PRIORITY_CATEGORY_ALARMS) 优先处理警报。
  - [`PRIORITY_CATEGORY_MEDIA`](https://developer.android.google.cn/reference/android/app/NotificationManager.Policy#PRIORITY_CATEGORY_MEDIA) 优先处理媒体源的声音，如媒体和语音导航。
  - [`PRIORITY_CATEGORY_SYSTEM`](https://developer.android.google.cn/reference/android/app/NotificationManager.Policy#PRIORITY_CATEGORY_SYSTEM) 优先处理系统声音。

- `NotificationManager.Policy` 还有 7 种新的“请勿打扰”常量，可以用来抑制视觉中断：

  - [`SUPPRESSED_EFFECT_FULL_SCREEN_INTENT`](https://developer.android.google.cn/reference/android/app/NotificationManager.Policy#SUPRESSED_EFFECT_FULL_SCREEN_INTENT) 防止通知启动全屏 Activity。
  - [`SUPPRESSED_EFFECT_LIGHTS`](https://developer.android.google.cn/reference/android/app/NotificationManager.Policy#SUPRESSED_EFFECT_LIGHTS) 屏蔽通知灯。
  - [`SUPPRESSED_EFFECT_PEEK`](https://developer.android.google.cn/reference/android/app/NotificationManager.Policy#SUPRESSED_EFFECT_PEEK) 防止通知短暂进入视图（“滑出”）。
  - [`SUPPRESSED_EFFECT_STATUS_BAR`](https://developer.android.google.cn/reference/android/app/NotificationManager.Policy#SUPRESSED_EFFECT_STATUS_BAR) 防止通知显示在支持状态栏的设备的状态栏中。
  - [`SUPPRESSED_EFFECT_BADGE`](https://developer.android.google.cn/reference/android/app/NotificationManager.Policy#SUPRESSED_EFFECT_BADGE) 在支持标志的设备上屏蔽标志。 如需了解详细信息，请参阅[修改通知标志](https://developer.android.google.cn/training/notify-user/badges.html)。
  - [`SUPPRESSED_EFFECT_AMBIENT`](https://developer.android.google.cn/reference/android/app/NotificationManager.Policy#SUPRESSED_EFFECT_AMBIENT) 在支持微光显示的设备上屏蔽通知。
  - [`SUPPRESSED_EFFECT_NOTIFICATION_LIST`](https://developer.android.google.cn/reference/android/app/NotificationManager.Policy#SUPRESSED_EFFECT_NOTIFICATION_LIST) 防止通知显示在支持列表视图（如通知栏或锁屏）的设备的列表视图中。

多摄像头支持和摄像头更新

在运行 Android 9 的设备上，您可以通过[两个或更多物理摄像头](https://developer.android.google.cn/reference/android/hardware/camera2/CameraMetadata#REQUEST_AVAILABLE_CAPABILITIES_LOGICAL_MULTI_CAMERA)来同时访问多个视频流。] 在配备双前置摄像头或双后置摄像头的设备上，您可以创建只配备单摄像头的设备所不可能实现的创新功能，例如无缝缩放、背景虚化和立体成像。 通过该 API，您还可以调用逻辑或融合的摄像头视频流，该视频流可在两个或更多摄像头之间自动切换。

摄像头方面的其他改进还包括附加[会话参数](https://developer.android.google.cn/reference/android/hardware/camera2/params/SessionConfiguration)和 Surface 共享，前者有助于降低首次拍照期间的延迟，而后者则让摄像头客户端能够处理各种用例，而无需停止并启动摄像头视频流。 我们还针对基于显示屏的 [flash 支持](https://developer.android.google.cn/reference/android/hardware/camera2/CameraMetadata#CONTROL_AE_MODE_ON_EXTERNAL_FLASH)和 [OIS 时间戳](https://developer.android.google.cn/reference/android/hardware/camera2/CaptureResult#STATISTICS_OIS_TIMESTAMPS)访问新增了一些 API，用以实现应用级的图像稳定化和特效。

在 Android 9 中，[多摄像头 API](https://developer.android.google.cn/reference/android/hardware/camera2/CameraMetadata#REQUEST_AVAILABLE_CAPABILITIES_LOGICAL_MULTI_CAMERA)支持单色摄像头，适用于具有 `FULL` 或 `LIMITED` 功能的设备。 单色输出通过 `YUV_420_888` 格式实现，Y 为灰度，U (Cb) 为 128，V (Cr) 为 128。

在受支持的设备上，Android 9 还支持[外置 USB/UVC 摄像头](https://developer.android.google.cn/reference/android/hardware/camera2/CameraCharacteristics)。

适用于可绘制对象和位图的 ImageDecoder

Android 9 引入了 [`ImageDecoder`](https://developer.android.google.cn/reference/android/graphics/ImageDecoder) 类，可提供现代化的图像解码方法。 使用该类取代 [`BitmapFactory`](https://developer.android.google.cn/reference/android/graphics/BitmapFactory) 和 [`BitmapFactory.Options`](https://developer.android.google.cn/reference/android/graphics/BitmapFactory.Options) API。

`ImageDecoder` 让您可通过字节缓冲区、文件或 URI 来创建 [`Drawable`](https://developer.android.google.cn/reference/android/graphics/drawable/Drawable) 或 [`Bitmap`](https://developer.android.google.cn/reference/android/graphics/Bitmap)。 要解码图像，请首先以编码图像的来源为参数，调用 [`createSource()`](https://developer.android.google.cn/reference/android/graphics/ImageDecoder#createSource(java.nio.ByteBuffer))。 然后，通过传递 [`ImageDecoder.Source`](https://developer.android.google.cn/reference/android/graphics/ImageDecoder.Source) 对象来调用 [`decodeDrawable()`](https://developer.android.google.cn/reference/android/graphics/ImageDecoder#decodeDrawable(android.graphics.ImageDecoder.Source)) 或 [`decodeBitmap()`](https://developer.android.google.cn/reference/android/graphics/ImageDecoder#decodeBitmap(android.graphics.ImageDecoder.Source))，从而创建 `Drawable`] 或 `Bitmap`。 要更改默认设置，请将 [`OnHeaderDecodedListener`](https://developer.android.google.cn/reference/android/graphics/ImageDecoder.OnHeaderDecodedListener) 传递给 `decodeDrawable()` 或 `decodeBitmap()`。 `ImageDecoder` 调用 [`onHeaderDecoded()`](https://developer.android.google.cn/reference/android/graphics/ImageDecoder.OnHeaderDecodedListener#onHeaderDecoded(android.graphics.ImageDecoder, android.graphics.ImageDecoder.ImageInfo, android.graphics.ImageDecoder.Source))，以图像的默认宽度和高度（若已知）为参数。 如果编码图像是动画 GIF 或 WebP，`decodeDrawable()` 将返回 `Drawable`，它是 [`AnimatedImageDrawable`](https://developer.android.google.cn/reference/android/graphics/drawable/AnimatedImageDrawable) 类的一个实例。

您可以使用不同的方法来设置图像属性：

- 要将解码的图像缩放到精确尺寸，请将目标尺寸传递给 [`setTargetSize()`](https://developer.android.google.cn/reference/android/graphics/ImageDecoder#setTargetSize(int, int))。 您也可以使用样图尺寸来缩放图像。 将样图尺寸直接传递给 [`setTargetSampleSize()`](https://developer.android.google.cn/reference/android/graphics/ImageDecoder#setTargetSampleSize(int))。
- 要在缩放图像的范围内裁剪图像，请调用 [`setCrop()`](https://developer.android.google.cn/reference/android/graphics/ImageDecoder#setCrop(android.graphics.Rect))。
- 要创建可变位图，请将 `true` 传递给 [`setMutableRequired()`](https://developer.android.google.cn/reference/android/graphics/ImageDecoder#setMutableRequired(boolean))。

通过 `ImageDecoder` 还可以为圆角或圆形遮罩之类的图像添加复杂的定制效果。 以 [`PostProcessor`](https://developer.android.google.cn/reference/android/graphics/PostProcessor) 类的一个实例作为参数使用 [`setPostProcessor()`](https://developer.android.google.cn/reference/android/graphics/ImageDecoder#setPostProcessor(android.graphics.PostProcessor))，执行您所需的任何绘图命令。

注：对 [`AnimatedImageDrawable`](https://developer.android.google.cn/reference/android/graphics/drawable/AnimatedImageDrawable)进行后处理时，效果会出现在动画的所有帧中。

动画

Android 9 引入了 [`AnimatedImageDrawable`](https://developer.android.google.cn/reference/android/graphics/drawable/AnimatedImageDrawable) 类，用于绘制和显示 GIF 和 WebP 动画图像。 `AnimatedImageDrawable` 的工作方式与 [`AnimatedVectorDrawable`](https://developer.android.google.cn/reference/android/graphics/drawable/AnimatedVectorDrawable) 的相似之处在于，都是渲染线程驱动 `AnimatedImageDrawable` 的动画。 渲染线程还使用工作线程进行解码，因此，解码不会干扰渲染线程的其他操作。 这种实现机制允许您的应用在显示动画图像时，无需管理其更新，也不会干扰应用界面线程上的其他事件。

可使用 [`ImageDecoder`](https://developer.android.google.cn/reference/android/graphics/ImageDecoder) 的实例对 `AnimatedImageDrawable` 进行解码。 以下代码段演示如何使用 `ImageDecoder` 来解码`AnimatedImageDrawable`：

[KOTLIN](https://developer.android.google.cn/about/versions/pie/android-9.0#kotlin)

[JAVA](https://developer.android.google.cn/about/versions/pie/android-9.0#java)

```
@Throws(IOException::class)
private fun decodeImage() {
    val decodedAnimation = ImageDecoder.decodeDrawable(
        ImageDecoder.createSource(resources, R.drawable.my_drawable))

    // Prior to start(), the first frame is displayed.
    (decodedAnimation as? AnimatedImageDrawable)?.start()
}
```

`ImageDecoder` 有几个允许您进一步修改图像的函数。 例如，可使用 [`setPostProcessor()`](https://developer.android.google.cn/reference/android/graphics/ImageDecoder#setPostProcessor(android.graphics.PostProcessor)) 函数来修改图像的外观，如应用圆形遮罩或圆角。

HDR VP9 视频、HEIF 图像压缩和 Media API

Android 9 新增了对 High Dynamic Range (HDR) VP9 Profile 2 的内置支持，因此，现在您可以在支持 HDR 的设备上为用户提供来自 YouTube、Play Movies 和其他来源的采用 HDR 的影片。

Android 9 为平台增加了对 [HEIF](https://developer.android.google.cn/reference/android/media/MediaFormat#MIMETYPE_IMAGE_ANDROID_HEIC) (heic) 图像编码的支持。 [`MediaMuxer`](https://developer.android.google.cn/reference/android/media/MediaMuxer#addTrack(android.media.MediaFormat)) 和 [`MediaExtractor`](https://developer.android.google.cn/reference/android/media/MediaExtractor#getTrackFormat(int)) 类中可支持 HEIF 静态图像示例 HEIF 改进了压缩，可节省存储空间和网络数据流量。 借助 Android 9 设备上的平台支持，从后端服务器发送和使用 HEIF 图像轻而易举。 确保应用兼容这种便于共享和显示的数据格式后，尝试在应用中使用 HEIF 作为图像存储格式。 您可以使用 [ImageDecoder](https://developer.android.google.cn/reference/android/graphics/ImageDecoder) 或 [BitmapFactory](https://developer.android.google.cn/reference/android/graphics/BitmapFactory) 进行 jpeg 到 heicto 的转换，以通过 jpeg 获取位图，并且可以使用 [HeifWriter](https://developer.android.google.cn/reference/androidx/heifwriter/HeifWriter) 写入来自 YUV 字节缓冲区、Surface 或 Bitmap 的 HEIF 静态图像。

还可通过 [`AudioTrack`](https://developer.android.google.cn/reference/android/media/AudioTrack#getMetrics())、[`AudioRecord`](https://developer.android.google.cn/reference/android/media/AudioRecord#getMetrics()) 和 [`MediaDrm`](https://developer.android.google.cn/reference/android/media/MediaDrm#getMetrics()) 类获取媒体指标。

Android 9 向 [`MediaDRM`](https://developer.android.google.cn/reference/android/media/MediaDrm) 类添加了函数以获取指标、高带宽数字内容保护 (HDCP) 级别、安全级别和会话数，并对安全性级别和安全停止进行更多控制。 如需了解更多详情，请参阅 [API 差异报告](https://developer.android.google.cn/sdk/api_diff/p-dp1/changes)。

在 Android 9 中，[AAudio](https://developer.android.google.cn/ndk/guides/audio/aaudio/aaudio) API 包含 AAudioStream 属性，用于 [usage](https://developer.android.google.cn/ndk/reference/group___audio#ga7396148c8b2cc12948fdbc2d9f41048b)、[content type](https://developer.android.google.cn/ndk/reference/group___audio#gaaacaadf2c30559aebdd17d8a20954702) 和 [input preset](https://developer.android.google.cn/ndk/reference/group___audio#gac0265431d098dae804c44257481a4b66)。 使用这些属性可以创建针对 VoIP 或摄像机应用调整的流。 您还可以设置 [SessionID](https://developer.android.google.cn/ndk/reference/group___audio#ga40d35c053065700469def0bfd084a73e)将 AAudio 流与可包含音效的子混音相关联。 使用 `AudioEffect API` 来控制音效。

Android 9 包含一个用于 [DynamicsProcessing](https://developer.android.google.cn/reference/android/media/audiofx/DynamicsProcessing) 的 [AudioEffect](https://developer.android.google.cn/reference/android/media/audiofx/AudioEffect) API。 借助该类，可以构建基于通道的音效，由各种类型（包括均衡、多频带压缩和限幅器）的多个阶段组成。 频带和活动阶段的数量可配置，而且大多数参数可实时控制。

JobScheduler 中的流量费用敏感度

从 Android 9 开始，[`JobScheduler`](https://developer.android.google.cn/reference/android/app/job/JobScheduler) 可以使用运营商提供的网络状态信号来改善与网络有关的作业处理。

作业可以声明其预估的数据大小、信号预提取，并指定具体的网络要求。 `JobScheduler` 然后根据网络状态管理工作。 例如，当网络显示拥塞时，`JobScheduler` 可能会延迟较大的网络请求。 如果使用的是不按流量计费的网络，则 `JobScheduler` 可运行预提取作业以提升用户体验（例如预提取标题）。

添加作业时，确保使用 [`setEstimatedNetworkBytes()`](https://developer.android.google.cn/reference/android/app/job/JobInfo.Builder#setEstimatedNetworkBytes(long, long))、[`setPrefetch()`](https://developer.android.google.cn/reference/android/app/job/JobInfo.Builder#setPrefetch(boolean)) 和 [`setRequiredNetwork()`](https://developer.android.google.cn/reference/android/app/job/JobInfo.Builder#setRequiredNetwork(android.net.NetworkRequest))（如果适用），以帮助 `JobScheduler` 正确处理工作。 在执行作业时，请确保使用 [`JobParameters.getNetwork()`](https://developer.android.google.cn/reference/android/app/job/JobParameters#getNetwork()) 返回的 [`Network`](https://developer.android.google.cn/reference/android/net/Network) 对象。 否则，您将隐式使用设备的默认网络，其可能不符合您的要求，从而导致意外的流量消耗。

Neural Networks API 1.1

Android 8.1（API 级别 27）中引入了 [Neural Networks API](https://developer.android.google.cn/ndk/guides/neuralnetworks) 以加快 Android 设备上机器学习的速度。 Android 9 扩展和改进了该 API，增加了对九种新运算的支持：

- 元素级数学运算：
  - [`ANEURALNETWORKS_DIV`](https://developer.android.google.cn/ndk/reference/group/neural-networks#group___neural_networks_1ggaabbe492c60331b13038e39d4207940e0a139794099b4137599bbc73af18b0d42a)
  - [`ANEURALNETWORKS_SUB`](https://developer.android.google.cn/ndk/reference/group/neural-networks#group___neural_networks_1ggaabbe492c60331b13038e39d4207940e0a06a4248fe5ec71820ab95b87613780be)
- 数组运算：
  - [`ANEURALNETWORKS_BATCH_TO_SPACE_ND`](https://developer.android.google.cn/ndk/reference/group/neural-networks#group___neural_networks_1ggaabbe492c60331b13038e39d4207940e0a2bdfefbdc6409b4bbcacc16c72002703)
  - [`ANEURALNETWORKS_SPACE_TO_BATCH_ND`](https://developer.android.google.cn/ndk/reference/group/neural-networks#group___neural_networks_1ggaabbe492c60331b13038e39d4207940e0a91f17c92abe95e211de39c3715acd535)
  - [`ANEURALNETWORKS_SQUEEZE`](https://developer.android.google.cn/ndk/reference/group/neural-networks#group___neural_networks_1ggaabbe492c60331b13038e39d4207940e0a1207019989837ee9d10c5b6663504933)
  - [`ANEURALNETWORKS_STRIDED_SLICE`](https://developer.android.google.cn/ndk/reference/group/neural-networks#group___neural_networks_1ggaabbe492c60331b13038e39d4207940e0a89695302f8b1e7ae7ce8f4d8c0b8a752)
  - [`ANEURALNETWORKS_TRANSPOSE`](https://developer.android.google.cn/ndk/reference/group/neural-networks#group___neural_networks_1ggaabbe492c60331b13038e39d4207940e0a92d7bc95eb68525334b6cfe80cd271ee)
  - [`ANEURALNETWORKS_PAD`](https://developer.android.google.cn/ndk/reference/group/neural-networks#group___neural_networks_1ggaabbe492c60331b13038e39d4207940e0aaced01fc41e401b81cefcf53780558d1)
  - [`ANEURALNETWORKS_MEAN`](https://developer.android.google.cn/ndk/reference/group/neural-networks#group___neural_networks_1ggaabbe492c60331b13038e39d4207940e0a047fe95a35b27f45c05432b6ca18eb6c)

**已知问题：** 将 `ANEURALNETWORKS_TENSOR_QUANT8_ASYMM` 张量传递到 `ANEURALNETWORKS_PAD` 运算（在 Android 9 及更高版本中提供）时，NNAPI 的输出可能与较高级别机器学习框架（如 [TensorFlow Lite](https://tensorflow.google.cn/mobile/tflite/)）的输出不匹配。 应只传递 [`ANEURALNETWORKS_TENSOR_FLOAT32`](https://developer.android.google.cn/ndk/reference/group/neural-networks#group___neural_networks_1ggaf06d1affd33f3bc698d0c04eceb23298aee4bc05d71c31e22e39e05470e965447) 直到问题得到解决。

此外，API 还引入了一个新函数，即 [`ANeuralNetworksModel_relaxComputationFloat32toFloat16()`](https://developer.android.google.cn/ndk/reference/group/neural-networks#group___neural_networks_1gab822719f98f0c92e5da3684cdaca6ba0)，允许您指定是否计算范围和精度低至 IEEE 754 16 位浮点格式的 [`ANEURALNETWORKS_TENSOR_FLOAT32`](https://developer.android.google.cn/ndk/reference/group/neural-networks#group___neural_networks_1ggaf06d1affd33f3bc698d0c04eceb23298aee4bc05d71c31e22e39e05470e965447)。

自动填充框架

Android 9 引入了多项改进，自动填充服务可以利用这些改进进一步增强用户填写表单时的体验。 如需详细了解如何在您的应用中使用自动填充功能，请参阅[自动填充框架](https://developer.android.google.cn/guide/topics/text/autofill)指南。

安全增强功能

Android 9 引入了若干安全功能，详见以下各节摘要说明：

Android Protected Confirmation

运行 Android 9 或更高版本的受支持设备赋予您使用 Android Protected Confirmation 的能力。 使用该工作流时，您的应用会向用户显示提示，请他们批准一个简短的声明。 应用可以通过这个声明再次确认，用户确实想完成一项敏感事务，例如付款。

如果用户接受该声明，Android 密钥库会收到并存储由密钥哈希消息身份验证代码 (HMAC) 保护的加密签名。 Android 密钥库确认消息的有效性之后，您的应用可以使用在可信执行环境 (TEE) 下通过 `trustedConfirmationRequired` 生成的密钥来签署用户已接受的消息。 该签名具有很高的可信度，它表示用户已看过声明并同意其内容。

**注意：**Android Protected Confirmation 不会为用户提供安全信息通道。 应用无法承担 Android 平台所提供机密性保证之外的任何其他保证。 尤其是，请勿使用该工作流显示您通常不会显示在用户设备上的敏感信息。

如需获得 Android Protected Confirmation 新增支持方面的指导，请参阅 [Android Protected Confirmation](https://developer.android.google.cn/training/articles/security-android-protected-confirmation) 指南。

统一生物识别身份验证对话框

在 Android 9 中，系统代表您的应用提供生物识别身份验证对话框。 该功能可创建标准化的对话框外观、风格和位置，让用户更加确信，他们在使用可信的生物识别凭据检查程序进行身份验证。

如果您的应用使用 [`FingerprintManager`](https://developer.android.google.cn/reference/android/hardware/fingerprint/FingerprintManager) 向用户显示指纹身份验证对话框，请切换到改用 [`BiometricPrompt`](https://developer.android.google.cn/reference/android/hardware/biometrics/BiometricPrompt)。`BiometricPrompt` 依赖系统来显示身份验证对话框。 它还会改变其行为，以适应用户所选择的生物识别身份验证类型。

注：在应用中使用 `BiometricPrompt` 之前，应该先使用 [`hasSystemFeature()`](https://developer.android.google.cn/reference/android/content/pm/PackageManager#hasSystemFeature(java.lang.String))函数以确保设备支持 `FEATURE_FINGERPRINT`、`FEATURE_IRIS` 或 `FEATURE_FACE`。

如果设备不支持生物识别身份验证，可以回退为使用 [`createConfirmDeviceCredentialIntent()`](https://developer.android.google.cn/reference/android/app/KeyguardManager#createConfirmDeviceCredentialIntent(java.lang.CharSequence, java.lang.CharSequence)) 函数验证用户的 PIN 码、图案或密码。

硬件安全性模块

运行 Android 9 或更高版本的受支持设备可拥有 *StrongBox Keymaster*，它是位于硬件安全性模块中的 Keymaster HAL 的一种实现。 该模块包含以下组成部分：

- 自己的 CPU。
- 安全存储空间。
- 真实随机数生成器。
- 可抵御软件包篡改和未经授权线刷应用的附加机制。

检查存储在 StrongBox Keymaster 中的密钥时，系统会通过可信执行环境 (TEE) 证实密钥的完整性。

如需了解有关使用 Strongbox Keymaster 的更多信息，请参阅[硬件安全性模块](https://developer.android.google.cn/training/articles/keystore#HardwareSecurityModule)。

保护对密钥库进行的密钥导入

Android 9 通过利用 ASN.1‑编码密钥格式将已加密密钥安全导入密钥库的功能，提高了密钥解密的安全性。 Keymaster 随后会在密钥库中将密钥解密，因此密钥的内容永远不会以明文形式出现在设备的主机内存中。

注：只有附带 Keymaster 4 或更高版本的设备才支持该功能。

详细了解如何[更安全地导入已加密密钥](https://developer.android.google.cn/training/articles/keystore#ImportingEncryptedKeys)。

具有密钥轮转的 APK 签名方案

Android 9 新增了对 APK Signature Scheme v3 的支持。该架构提供的选择可以在其签名块中为每个签名证书加入一条轮转证据记录。 利用此功能，应用可以通过将 APK 文件过去的签名证书链接到现在签署应用时使用的证书，从而使用新签名证书来签署应用。

注：运行 Android 8.1（API 级别 27）或更低版本的设备不支持更改签名证书。 如果应用的 `minSdkVersion` 为 `27` 或更低，除了新签名之外，可使用旧签名证书来签署应用。

详细了解如何使用 [`apksigner`](https://developer.android.google.cn/studio/command-line/apksigner#usage-rotate) 轮转密钥。

只允许在未锁定设备上进行密钥解密的选项

Android 9 引入了 `unlockedDeviceRequired` 标志。 此选项确定在允许使用指定密钥对任何正在传输或存储的数据进行解密之前，密钥库是否要求屏幕解锁。 这些类型的密钥非常适合用于加密要存储在磁盘上的敏感数据，例如健康或企业数据。 该标志为用户提供了更高的保证，即使手机丢失或被盗，在设备锁定的情况下，无法对数据进行解密。

注：`unlockedDeviceRequired` 标志启用之后，仍然可以随时进行加密和签名验证。 该标志可防止在设备解锁时“仅解密”数据。

在设备锁定时要确保密钥安全不被解密，可通过将 `true` 传递给 [`setUnlockedDeviceRequired()`](https://developer.android.google.cn/reference/android/security/keystore/KeyGenParameterSpec.Builder#setUnlockedDeviceRequired(boolean)) 函数启用该标志。 完成该步骤之后，当用户的屏幕被锁定时，使用该密钥进行解密或签署数据的任何尝试都会失败。 锁定设备在可以访问之前，需要 PIN 码、密码、指纹或者一些其他可信因素。

旧版加密支持

附带 Keymaster 4 的 Android 9 设备支持三重数据加密算法（简称三重 DES）。 如果您的应用与需要三重 DES 的旧版系统进行互操作，请使用这种加密来加密敏感凭据。

如需详细了解如何让您的应用更加安全，请参阅 [Android 开发者的安全性](https://developer.android.google.cn/topic/security)。



Android 备份Android 9 新增了与备份和还原有关的功能和开发者选项。 这些更改的详细信息如以部分下所示。客户端加密备份Android 9 新增了对使用客户端密钥加密 Android 备份的支持。 满足下列条件时会自动启用该支持功能：

- 

- 用户已使用 Android 9 或更高版本[启用备份](https://support.google.com/pixelphone/answer/7179901)。
- 用户已为其设备[设置屏幕锁定](https://support.google.com/android/answer/2819522?hl=en)，需要 PIN 码、图案或密码才能解锁。

该隐私措施启用之后，从用户设备制作的备份还原数据时，会要求提供设备的 PIN 码、图案或密码。 如需详细了解该项功能背后的技术，请参阅 [Google 云密钥保险柜服务](https://developer.android.google.cn/about/versions/pie/security/ckv-whitepaper)白皮书。

定义备份所需的设备条件

如果您的应用数据包含敏感信息或偏好，Android 9 可让您[定义设备条件](https://developer.android.google.cn/guide/topics/data/autobackup#define-device-conditions)（例如在客户端加密已启用或者正在进行本地设备到设备传输时），数据将依据该条件包括在用户的备份中。

如需了解有关在 Android 设备上备份数据的详细信息，请参阅[数据备份概览](https://developer.android.google.cn/guide/topics/data/backup)。

无障碍功能

Android 9 引入了针对无障碍功能框架的增强功能，让您能够更轻松地为应用的用户提供更好的体验。

导航语义

Android 9 中的新增属性让您可以更轻松地定义无障碍服务（尤其是屏幕阅读器）如何从屏幕的某个部分导航到另一个部分。 这些属性可帮助视力受损用户在应用界面的文本之间快速移动，并允许他们进行选择。

例如，在购物应用中，屏幕阅读器可以帮助用户从某个交易类别直接导航至下一个交易类别，在转到下一个类别之前，屏幕阅读器无需读取当前类别中的所有交易。

无障碍功能窗格标题

在 Android 8.1（API 级别 27）和更低版本中，无障碍服务有时无法确定屏幕的某个窗格是何时更新的，例如某个 Activity 将一个 Fragment 替换为另一个 Fragment 的时候。 窗格由按照逻辑关系分组、视觉上相关的界面元素组成，其中通常包含一个 Fragment。

在 Android 9 中，可为这些窗格提供 *无障碍功能窗格标题*，即可单独识别的标题。 如果某个窗格具有无障碍功能窗格标题，当窗格改变时，无障碍服务可接收更详细的信息。 依靠这种功能，服务可以为用户提供有关界面变化的更精细信息。

要指定某个窗格的标题，请使用 [`android:accessibilityPaneTitle`](https://developer.android.google.cn/reference/android/R.attr#accessibilityPaneTitle) 属性。 您也可以更新在运行时使用 [`setAccessibilityPaneTitle()`](https://developer.android.google.cn/reference/android/view/View#setAccessibilityPaneTitle(java.lang.CharSequence)) 替换的某个界面窗格的标题。 例如，您可以为某个 [`Fragment`](https://developer.android.google.cn/reference/android/support/v4/app/Fragment) 对象的内容区域提供标题。

基于标题的导航

如果您的应用显示的文本内容包含逻辑标题，则对于表示这些标题的 [`View`](https://developer.android.google.cn/reference/android/view/View) 实例，请将[`android:accessibilityHeading`](https://developer.android.google.cn/reference/android/R.attr#accessibilityHeading) 属性设置为 `true`。 通过添加这些标题，无障碍服务可帮助用户直接从一个标题导航至下一个标题。 任何无障碍服务都可以使用这种功能，以改善用户界面的导航体验。

群组导航和输出

传统上，屏幕阅读器一直使用 [`android:focusable`](https://developer.android.google.cn/reference/android/R.attr#focusable) 属性来确定何时应该将 [`ViewGroup`](https://developer.android.google.cn/reference/android/view/ViewGroup) 或一系列 [`View`](https://developer.android.google.cn/reference/android/view/View) 对象作为一个整体进行读取。 这样，用户就可以了解，这些视图在逻辑上彼此相关。

在 Android 8.1 和更低版本中，您需要将 `ViewGroup` 中的每个 `View` 对象标记为不可聚焦，并将 `ViewGroup` 本身标记为可聚焦。 这种安排导致 `View` 的某些实例被标记为可聚焦，从而使得键盘导航变得更为繁琐。

从 Android 9 开始，如果将 `View` 对象标记为可聚焦会产生不良后果，则可以使用 [`android:screenReaderFocusable`](https://developer.android.google.cn/reference/android/R.attr#screenReaderFocusable) 属性代替 `android:focusable` 属性。 屏幕阅读器聚焦在所有将 `android:screenReaderFocusable` 或 `android:focusable` 设置为 `true` 的元素上。

便捷操作

Android 9 新增了一些方便用户执行操作的支持功能：

访问提示： 无障碍功能框架中的新增功能可让您在应用界面中访问[提示](https://developer.android.google.cn/guide/topics/ui/tooltips)。 使用 [`getTooltipText()`](https://developer.android.google.cn/reference/android/view/accessibility/AccessibilityNodeInfo#getTooltipText()) 读取提示文本，使用 [`ACTION_SHOW_TOOLTIP`](https://developer.android.google.cn/reference/android/view/accessibility/AccessibilityNodeInfo.AccessibilityAction#ACTION_SHOW_TOOLTIP) 和 [`ACTION_HIDE_TOOLTIP`](https://developer.android.google.cn/reference/android/view/accessibility/AccessibilityNodeInfo.AccessibilityAction#ACTION_HIDE_TOOLTIP) 来指示 [`View`](https://developer.android.google.cn/reference/android/view/View) 的实例显示或隐藏提示。

新增全局操作： Android 9 在 [`AccessibilityService`](https://developer.android.google.cn/reference/android/accessibilityservice/AccessibilityService) 类中引入了对两个额外设备操作的支持。 您的 Service 可以帮助用户分别使用 [`GLOBAL_ACTION_LOCK_SCREEN`](https://developer.android.google.cn/reference/android/accessibilityservice/AccessibilityService#GLOBAL_ACTION_LOCK_SCREEN) 和 [`GLOBAL_ACTION_TAKE_SCREENSHOT`](https://developer.android.google.cn/reference/android/accessibilityservice/AccessibilityService#GLOBAL_ACTION_TAKE_SCREENSHOT) 操作锁定其设备并进行屏幕截图。

窗口变更详情

Android 9 让您可以在应用同时重绘多个窗口时，更轻松地跟踪应用窗口的更新。 当发生 [`TYPE_WINDOWS_CHANGED`](https://developer.android.google.cn/reference/android/view/accessibility/AccessibilityEvent#TYPE_WINDOWS_CHANGED) 事件时，可使用 [`getWindowChanges()`](https://developer.android.google.cn/reference/android/view/accessibility/AccessibilityEvent#getWindowChanges()) API 来确定窗口发生的变更。 在多窗口更新期间，每个窗口都会生成自己的一组事件。[`getSource()`](https://developer.android.google.cn/reference/android/view/accessibility/AccessibilityRecord#getSource()) 函数返回与每个事件相关联的窗口的根视图。

如果应用已为其 [`View`](https://developer.android.google.cn/reference/android/view/View) 对象定义[无障碍功能窗格标题](https://developer.android.google.cn/about/versions/pie/android-9.0#a11y-pane-titles)，您的 Service 将可以识别应用界面何时进行更新。[`TYPE_WINDOW_STATE_CHANGED`](https://developer.android.google.cn/reference/android/view/accessibility/AccessibilityEvent#TYPE_WINDOW_STATE_CHANGED) 事件发生时，可使用 [`getContentChangeTypes()`](https://developer.android.google.cn/reference/android/view/accessibility/AccessibilityEvent#getContentChangeTypes()) 所返回的类型来确定窗口发生的变更。 例如，框架可以检测窗格何时有新标题或者窗格何时消失。

Google 致力于为所有 Android 用户改善无障碍功能，提供增强功能以便让您构建 Service，如[话语提示](https://support.google.com/accessibility/android/answer/6283677) 屏幕阅读器，供需要无障碍功能的用户使用。 如需了解有关如何让您的应用更便于访问以及如何构建无障碍 Service 的更多信息，请参阅[无障碍功能](https://developer.android.google.cn/guide/topics/ui/accessibility)。

旋转

为避免无意的旋转，我们新增了一种模式，哪怕设备位置发生变化，也会固定在当前屏幕方向上。 必要时用户可以通过按系统栏上的一个按钮手动触发旋转。

大多数情况下，对应用的兼容性影响微不足道。 不过，如果您的应用有任何自定义旋转行为，或使用了任何非常规的屏幕方向设置，则可能会遇到以前用户旋转首选项始终设置为纵向时被忽视的问题。 我们鼓励您审视一下您的应用所有关键 Activity 中的旋转行为，并确保您的所有屏幕方向设置仍可提供最佳体验。

如需了解更多详情，请参阅相关的[行为变更](https://developer.android.google.cn/preview/behavior-changes#screen-rotation-changes)。

![img](https://developer.android.google.cn/preview/images/rotate-changes.gif)

一个新的旋转模式允许用户在必要时利用系统栏上的一个按钮手动触发旋转。

文本

Android 9 为平台提供了以下与文本相关的功能：

- 文本预先计算：[`PrecomputedText`](https://developer.android.google.cn/reference/android/text/PrecomputedText) 类使您能提前计算和缓存所需信息，改善了文本渲染性能。 它还使您的应用可以在主线程之外执行文本布局。
- 放大器：[`Magnifier`](https://developer.android.google.cn/reference/android/widget/Magnifier) 类是一种可提供放大器 API 的微件，可在所有应用中实现一致的放大器功能体验。
- Smart Linkify：Android 9 增强了 [`TextClassifier`](https://developer.android.google.cn/reference/android/view/textclassifier/TextClassifier) 类，该类可利用机器学习在选定文本中识别一些实体并建议采取相应的操作。 例如，`TextClassifier` 可以让您的应用检测到用户选择了电话号码。 然后，您的应用可以建议用户使用该号码拨打电话。 `TextClassifier` 中的功能取代了 `Linkify` 类的功能。
- 文本布局：借助几种便捷函数和属性，可以更轻松地实现界面设计。 如需了解详细信息，请参阅 [`TextView`](https://developer.android.google.cn/reference/android/widget/TextView) 参考文档。

DEX 文件的 ART 提前转换

在运行 Android 9 或更高版本的设备上，Android 运行时 (ART) 提前编译器通过将应用软件包中的 DEX 文件转换为更紧凑的表示形式，进一步优化了压缩的 Dalvik Executable 格式 (DEX) 文件。 此项变更可让您的应用启动更快并消耗更少的磁盘空间和内存。

这种改进特别有利于磁盘 I/O 速度较慢的低端设备。

设备端系统跟踪

Android 9 允许您通过设备记录系统跟踪记录，然后与您的开发团队分享这些记录的报告。 该报告支持多种格式，包括 HTML。