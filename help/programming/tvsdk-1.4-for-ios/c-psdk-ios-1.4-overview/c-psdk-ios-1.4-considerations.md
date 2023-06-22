---
description: 为了最有效地使用TVSDK，您应考虑其操作的某些详细信息并遵循某些最佳实践。
title: 注意事项和最佳实践
exl-id: d10532a5-bf96-4233-86f1-b135f6e1c0f5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# 注意事项和最佳实践{#considerations-and-best-practices}

为了最有效地使用TVSDK，您应考虑其操作的某些详细信息并遵循某些最佳实践。

## 注意事项 {#section_tvsdk_considerations}

使用TVSDK时，请记住以下信息：

* Adobe Primetime在iOS模拟器上不起作用。

   您必须使用真实设备进行测试。
* 仅HTTP实时流(HLS)内容支持播放。
* 主视频内容可以多路复用，其中视频和音频流位于同一演绎版；也可以非多路复用，其中视频和音频流位于单独的演绎版。
* TVSDK API在Objective-C中实现。
* 视频播放需要本机Apple AV Foundation框架。 这会影响访问媒体资源（包括隐藏式字幕和时间线）的方式和时间：

   * 在初始设置后，无法修订时间线调整。

      例如，播发在播放后无法从时间轴中删除。 如果用户重新在演示文稿中搜索，则即使策略本来是删除该广告，也会再次播放相同的广告。
   * 根据编码器精度，实际的编码媒体持续时间可能与流资源清单中记录的持续时间不同。

      没有可靠的方法可以在理想的虚拟时间轴和实际的播放时间轴之间重新同步。 广告管理和视频分析的流播放进度跟踪必须使用实际播放时间，因此报告和用户界面行为可能无法准确跟踪媒体和广告内容。
   * 此平台上TVSDK发出的所有HTTP请求的传入用户代理由设备以及该设备上运行的iOS版本决定。

      用户代理字符串的值默认为操作系统分配的内容。

## 最佳实践 {#section_tvsdk_best_practices}

以下是TVSDK的建议实践：

* 对程序内容使用HLS版本3.0或更高版本。
* 使用Apple的mediastreamvalidator工具验证VOD流。
* 此 `PTSDKConfig` 类提供了在向Primetime Ad Decisioning、DRM和Video Analytics服务器发出的请求上实施SSL的方法。

   欲了解更多信息，请参见 `forceHTTPS` 和 `isForcingHTTPS` 类中的方法。

   >[!IMPORTANT]
   >
   >不会修改对第三方域（如广告跟踪像素、内容和广告URL）的请求以及类似请求。 内容提供商和广告服务器负责提供通过HTTPS支持的URL。
