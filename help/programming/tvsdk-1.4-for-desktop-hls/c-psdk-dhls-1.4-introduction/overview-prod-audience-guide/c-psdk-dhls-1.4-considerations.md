---
description: 要最有效地使用TVSDK，您应考虑其操作的某些细节并遵循某些最佳实践。
title: 注意事项和最佳实践
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---


# 注意事项和最佳实践{#considerations-and-best-practices}

要最有效地使用TVSDK，您应考虑其操作的某些细节并遵循某些最佳实践。

## 注意事项{#section_tvsdk_considerations}

使用TVSDK时，请记住以下信息：

* Adobe Primetime在模拟器或模拟器上不工作。

   必须使用真正的设备进行测试。
* 仅支持HTTP实时流(HLS)内容播放。
* 主视频内容可以被复用，其中视频和音频流位于相同的再现中，或者不被复用，其中视频和音频流位于不同的再现中。
* TVSDK API在ActionScript中实现。
* Adobe播放需要视频引擎(AVE)。 这会影响访问媒体资源的方式和时间：

   * 在AVE提供的范围内支持隐藏式字幕。
   * 根据编码器精度，实际编码媒体持续时间可能不同于流资源清单中记录的持续时间。

      在理想的虚拟时间线和实际播放时间线之间重新同步没有可靠的方法。 用于广告管理和视频分析的流播放的进度跟踪必须使用实际播放时间，因此报告和用户界面行为可能无法精确跟踪媒体和广告内容。
   * 此平台上来自TVSDK的所有HTTP请求的传入用户代理名称分配了以下字符串模式：

      ```
      "Adobe Flash Player"
      ```

## 最佳实践{#section_tvsdk_best_practices}

以下是TVSDK的推荐做法：

* 将HLS 3.0版或更高版本用于项目内容。
* 对于DHLS的TVSDK 1.4，默认情况下启用延迟广告加载。

   对于没有前置或中置的内容，您可以使用`AdvertisingMetadata.delayAdLoading`进一步加快内容加载。

