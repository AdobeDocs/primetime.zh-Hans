---
description: 要最有效地使用TVSDK，您应考虑其操作的某些详细信息并遵循某些最佳实践。
seo-description: 要最有效地使用TVSDK，您应考虑其操作的某些详细信息并遵循某些最佳实践。
seo-title: 注意事项和最佳实践
title: 注意事项和最佳实践
uuid: 62a5d641-6f37-4e4d-bbc2-414bf3681d9c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 注意事项和最佳实践{#considerations-and-best-practices}

要最有效地使用TVSDK，您应考虑其操作的某些详细信息并遵循某些最佳实践。

## 注意事项 {#section_tvsdk_considerations}

使用TVSDK时，请记住以下信息：

* Adobe Primetime不适用于模拟器或模拟器。

   您必须使用真正的设备进行测试。
* 仅HTTP实时流(HLS)内容支持播放。
* 主视频内容可以被多路复用，其中视频和音频流位于同一再现中，或者非多路复用，其中视频和音频流位于单独的再现中。
* TVSDK API在ActionScript中实现。
* 视频回放需要Adobe视频引擎(AVE)。 这会影响访问媒体资源的方式和时间：

   * 在AVE提供的范围内支持隐藏式字幕。
   * 根据编码器精度，实际编码媒体持续时间可能与流资源清单中记录的持续时间不同。

      在理想的虚拟时间线和实际播放时间线之间重新同步没有可靠的方法。 用于广告管理和视频分析的流播放的进度跟踪必须使用实际的播放时间，因此报告和用户界面行为可能无法精确跟踪媒体和广告内容。
   * 此平台上来自TVSDK的所有HTTP请求的传入用户代理名称将分配以下字符串模式：

      ```
      "Adobe Flash Player"
      ```

## 最佳实践 {#section_tvsdk_best_practices}

以下是TVSDK的建议实践：

* 将HLS版本3.0或更高版本用于程序内容。
* 对于TVSDK 1.4 for DHLS，默认情况下启用延迟广告加载。

   对于没有预卷或中间卷的内容，您可以使用它加 `AdvertisingMetadata.delayAdLoading` 快内容加载的速度。

