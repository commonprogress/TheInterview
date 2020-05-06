# Android 6.0 新特性

1. ## 运行时权限

1. ## 低电耗模式和应用待机模式

2. ## 取消支持 Apache HTTP 客户端

3. ## BoringSSL

4. ## 硬件标识符访问权

5. ## 通知

6. ## 音频管理器变更

7. ## 浏览器书签变更

8. ## Android 密钥库变更

9. ## WLAN 和网络连接变更

10. ## 相机服务变更

11. ## 运行时

12. ## APK 验证

13. ## USB 连接

14. ## Android for Work 变更



​            **************** 详解  *********



1. 运行时权限：此版本Android 6.0（API 级别 23）引入了一种新的权限模式，用户可直接在运行时管理应用权限。这种模式让用户能够更好地了解和控制权限，同时为应用开发者精简了安装和自动更新过程。用户可为所安装的各个应用分别授予或撤销权限。
2. 低电耗模式和应用待机模式：版本引入了针对空闲设备和应用的最新节能优化技术。
3. 取消支持 Apache HTTP 客户端：Android 6.0 版移除了对 Apache HTTP 客户端的支持，如果您的应用使用该客户端，并以 Android 2.3（API 级别 9）或更高版本为目标平台，请改用 HttpURLConnection 类。
4. BoringSSL：Android 正在从使用 OpenSSL 库转向使用 [BoringSSL](https://link.jianshu.com/?t=https://boringssl.googlesource.com/boringssl/) 库。如果您要在应用中使用 Android NDK，请勿链接到并非 NDK API 组成部分的加密库，如 libcrypto.so 和 libssl.so。这些库并非公共 API，可能会在不同版本和设备上毫无征兆地发生变化或出现故障。此外，您还可能让自己暴露在安全漏洞的风险之下。请改为修改原生代码，以通过 JNI 调用 Java 加密 API，或静态链接到您选择的加密库。
5. 硬件标识符访问权：此版本开始，对于使用 WLAN API 和 Bluetooth API 的应用，Android 移除了对设备本地硬件标识符的编程访问权。WifiInfo.getMacAddress() 方法和 BluetoothAdapter.getAddress() 方法。
6. 通知：此版本移除了 Notification.setLatestEventInfo() 方法。请改用 Notification.Builder 类来构建通知。要重复更新通知，请重复使用 Notification.Builder 实例。调用 build() 方法可获取更新后的 Notification 实例。
7. 音频管理器变更:不再支持通过 AudioManager 类直接设置音量或将特定音频流静音。setStreamSolo() 方法已弃用，您应该改为调用 requestAudioFocus() 方法。类似地，setStreamMute() 方法也已弃用，请改为调用 adjustStreamVolume() 方法并传入方向值 ADJUST_MUTE 或 ADJUST_UNMUTE。
8. .......





Android面试题