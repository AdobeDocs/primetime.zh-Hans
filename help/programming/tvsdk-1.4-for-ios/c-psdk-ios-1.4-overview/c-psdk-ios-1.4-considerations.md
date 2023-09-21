---
description: 为了最有效地使用TVSDK，您应考虑其操作的某些详细信息并遵循某些最佳实践。
title: 注意事项和最佳实践
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# 注意事项和最佳实践{#considerations-and-best-practices}

为了最有效地使用TVSDK，您应考虑其操作的某些详细信息并遵循某些最佳实践。

## 注意事项 {#section_tvsdk_considerations}

使用TVSDK时，请记住以下信息：

* Adobe Primetime不适用于iOS模拟器。

  必须使用真实设备进行测试。
* 仅HTTP实时流(HLS)内容支持播放。
* 主视频内容可以是多路复用的，其中视频和音频流位于相同的演绎版；也可以是非多路复用的，其中视频和音频流位于不同的演绎版。
* TVSDK API在Objective-C中实现。
* 视频播放需要使用本机Apple AV Foundation框架。 这会影响访问媒体资源（包括隐藏式字幕和时间线）的方式和时间：

   * 在初始设置后，无法修订时间线调整。

     例如，播发在播放后无法从时间轴中删除。 如果用户试图在演示文稿中再次播放该广告，则即使策略本应删除该广告，也会再次播放该广告。
   * 根据编码器精度，实际的编码媒体持续时间可能与流资源清单中记录的持续时间不同。

     在理想的虚拟时间轴和实际的播放时间轴之间没有可靠的重新同步方法。 广告管理和视频分析的流播放进度跟踪必须使用实际播放时间，因此报告和用户界面行为可能无法准确跟踪媒体和广告内容。
   * 此平台上TVSDK发出的所有HTTP请求的传入用户代理由设备以及该设备上运行的iOS版本决定。

     用户代理字符串的值默认为操作系统分配的内容。

## 最佳实践 {#section_tvsdk_best_practices}

以下是TVSDK的建议实践：

* 对程序内容使用HLS版本3.0或更高版本。
* 使用Apple的mediastreamvalidator工具验证VOD流。
* 此 `PTSDKConfig` 类提供了在向Primetime ad decisioning、DRM和Video Analytics服务器发出的请求上实施SSL的方法。

  欲了解更多信息，请参见 `forceHTTPS` 和 `isForcingHTTPS` 此类中的方法。

  >[!IMPORTANT]
  >
  >不会修改对第三方域（如广告跟踪像素、内容和广告URL）的请求以及类似请求。 内容提供商和广告服务器负责提供通过HTTPS支持的URL。
