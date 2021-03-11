---
description: 要最有效地使用TVSDK，您应考虑其操作的某些细节并遵循某些最佳实践。
title: 注意事项和最佳实践
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---


# 注意事项和最佳实践{#considerations-and-best-practices}

要最有效地使用TVSDK，您应考虑其操作的某些细节并遵循某些最佳实践。

## 注意事项{#section_tvsdk_considerations}

使用TVSDK时，请记住以下信息：

* Adobe Primetime在iOS模拟器上不工作。

   必须使用真正的设备进行测试。
* 仅支持HTTP实时流(HLS)内容播放。
* 主视频内容可以被复用，其中视频和音频流位于同一再现中，或者不被复用，其中视频和音频流位于单独的再现中。
* TVSDK API在Objective-C中实现。
* 视频播放需要本机Apple AV Foundation框架。 这会影响访问媒体资源（包括隐藏字幕和时间轴）的方式和时间：

   * 无法在初始设置后修改时间轴调整。

      例如，播放播发后，无法从时间轴中删除播发。 如果用户在演示文稿中搜索，则即使策略是删除广告，也会再次播放同一广告。
   * 根据编码器精度，实际编码媒体持续时间可能不同于流资源清单中记录的持续时间。

      在理想的虚拟时间线和实际播放时间线之间重新同步没有可靠的方法。 用于广告管理和视频分析的流播放的进度跟踪必须使用实际播放时间，因此报告和用户界面行为可能无法精确跟踪媒体和广告内容。
   * 此平台上来自TVSDK的所有HTTP请求的传入用户代理由设备和设备上运行的iOS版本决定。

      用户代理字符串的值默认为操作系统分配的值。

## 最佳实践{#section_tvsdk_best_practices}

以下是TVSDK的推荐做法：

* 将HLS 3.0版或更高版本用于项目内容。
* 使用Apple的mediastreamvalidator工具验证VOD流。
* `PTSDKConfig`类提供对发往Primetime广告决策、DRM和视频分析服务器的请求实施SSL的方法。

   有关详细信息，请参阅此类中的`forceHTTPS`和`isForcingHTTPS`方法。

   >[!IMPORTANT]
   >
   >不会修改对第三方域（如广告跟踪像素、内容和广告URL）的请求以及类似请求。 内容提供者和广告服务器有责任提供通过HTTPS支持的URL。

