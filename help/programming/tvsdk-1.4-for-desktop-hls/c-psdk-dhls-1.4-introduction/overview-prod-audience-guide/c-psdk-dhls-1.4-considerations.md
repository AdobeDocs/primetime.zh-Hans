---
description: 为了最有效地使用TVSDK，您应考虑其操作的某些详细信息并遵循某些最佳实践。
title: 注意事项和最佳实践
exl-id: 5e1e09e1-f22e-4797-807a-14dbf50bb835
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# 注意事项和最佳实践{#considerations-and-best-practices}

为了最有效地使用TVSDK，您应考虑其操作的某些详细信息并遵循某些最佳实践。

## 注意事项 {#section_tvsdk_considerations}

使用TVSDK时，请记住以下信息：

* Adobe Primetime不适用于模拟器或模拟器。

   您必须使用真实设备进行测试。
* 仅HTTP实时流(HLS)内容支持播放。
* 主视频内容可以多路复用，其中视频和音频流位于同一演绎版；也可以非多路复用，其中视频和音频流位于单独的演绎版。
* TVSDK API采用ActionScript实现。
* 视频播放需要Adobe视频引擎(AVE)。 这会影响访问媒体资源的方式和时间：

   * 在AVE提供的范围内支持隐藏式字幕。
   * 根据编码器精度，实际的编码媒体持续时间可能与流资源清单中记录的持续时间不同。

      没有可靠的方法可以在理想的虚拟时间轴和实际的播放时间轴之间重新同步。 广告管理和视频分析的流播放进度跟踪必须使用实际播放时间，因此报告和用户界面行为可能无法准确跟踪媒体和广告内容。
   * 来自此平台TVSDK的所有HTTP请求的传入用户代理名称分配了以下字符串模式：

      ```
      "Adobe Flash Player"
      ```

## 最佳实践 {#section_tvsdk_best_practices}

以下是TVSDK的建议实践：

* 对程序内容使用HLS版本3.0或更高版本。
* 对于DHLS的TVSDK 1.4，默认启用延迟广告加载。

   对于没有前置或中置的内容，您可以使用 `AdvertisingMetadata.delayAdLoading` 以进一步加快内容加载。
