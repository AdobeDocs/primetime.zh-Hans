---
description: 要最有效地使用TVSDK，您应考虑其操作的某些详细信息并遵循某些最佳实践。
seo-description: 要最有效地使用TVSDK，您应考虑其操作的某些详细信息并遵循某些最佳实践。
seo-title: 注意事项和最佳实践
title: 注意事项和最佳实践
uuid: a65c9739-ed83-4519-8ae5-7ba4c8f1ca49
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 注意事项和最佳实践 {#considerations-and-best-practices}

要最有效地使用TVSDK，您应考虑其操作的某些详细信息并遵循某些最佳实践。

## 注意事项 {#section_tvsdk_considerations}

使用TVSDK时，请记住以下信息：

* TVSDK API是在Java中实现的。
* Adobe Primetime目前不支持Android模拟器。

   您必须使用真正的设备进行测试。
* 仅HTTP实时流(HLS)内容支持播放。
* 主视频内容可以被多路复用（在同一再现中的视频和音频流）或非多路复用（在单独再现中的视频和音频流）。
* 当前，您需要在UI线程（即主Android线程）上运行大多数TVSDK API操作。

   在主线程上正确运行的操作可能会引发错误，并在后台线程上运行时退出。
* 视频回放需要Adobe视频引擎(AVE)。 这会影响访问媒体资源的方式和时间：

   * 在AVE提供的范围内支持隐藏式字幕。
   * 根据编码器精度，实际编码媒体持续时间可能与流资源清单中记录的持续时间不同。

      在理想的虚拟时间线和实际播放时间线之间重新同步没有可靠的方法。 用于广告管理和视频分析的流播放的进度跟踪必须使用实际的播放时间，因此报告和用户界面行为可能无法精确跟踪媒体和广告内容。
   * 从此平台上的TVSDK发出的所有媒体请求的传入用户代理名称将分配以下字符串模式：

      ```
      "Adobe Primetime/" + originalUserAgent
      ```

      如果您在设置广告插入元数据时设置了所有广告相关调用，则使用Android默认用户代理或自定义用户代理。

## 最佳实践 {#section_tvsdk_best_practices}

以下是TVSDK的建议实践：

* 将HLS版本3.0或更高版本用于程序内容。
* 在主(UI)线程（而非后台线程）上运行大多数TVSDK操作。
* 对于适用于Android的TVSDK 3.0，默认情况下开启延迟广告解析。

对于没有预卷或中卷的内容，您可以使用它加 `AdvertisingMetadata.setPreroll(false)` 快内容加载。