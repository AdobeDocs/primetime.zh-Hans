---
description: 为了最有效地使用TVSDK，您应考虑其操作的某些详细信息并遵循某些最佳实践。
title: 注意事项和最佳实践
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# 注意事项和最佳实践 {#considerations-and-best-practices}

为了最有效地使用TVSDK，您应考虑其操作的某些详细信息并遵循某些最佳实践。

## 注意事项 {#section_tvsdk_considerations}

使用TVSDK时，请记住以下信息：

* TVSDK API使用Java实现。
* Adobe Primetime目前在Android模拟器上不起作用。

  必须使用真实设备进行测试。
* 仅HTTP实时流(HLS)内容支持播放。
* 主视频内容可以多路复用（同一节目中的视频和音频流）或非多路复用（单独的节目中的视频和音频流）。
* 目前，您需要在用户界面线程（主要Android线程）上运行大多数TVSDK API操作。

  在主线程上正确运行的操作可能会引发错误，并在后台线程上运行时退出。
* 视频播放需要Adobe视频引擎(AVE)。 这会影响访问媒体资源的方式和时间：

   * 在AVE提供的范围内支持隐藏式字幕。
   * 根据编码器精度，实际的编码媒体持续时间可能与流资源清单中记录的持续时间不同。

     在理想的虚拟时间轴和实际的播放时间轴之间没有可靠的重新同步方法。 广告管理和视频分析的流播放进度跟踪必须使用实际播放时间，因此报告和用户界面行为可能无法准确跟踪媒体和广告内容。
   * 来自此平台上TVSDK的所有媒体请求的传入用户代理名称将分配以下字符串模式：

     ```
     "Adobe Primetime/" + originalUserAgent
     ```

     如果在设置广告插入元数据时设置了Android默认用户代理或自定义用户代理，则所有与广告相关的调用都将使用该代理。

## 最佳实践 {#section_tvsdk_best_practices}

以下是TVSDK的建议实践：

* 对程序内容使用HLS版本3.0或更高版本。
* 在主(UI)线程（而非后台线程）上运行大多数TVSDK操作。
* 对于适用于Android的TVSDK 3.0，默认情况下会启用延迟广告解析。

对于没有前置或中置的内容，您可以使用 `AdvertisingMetadata.setPreroll(false)` 以加速内容加载。
