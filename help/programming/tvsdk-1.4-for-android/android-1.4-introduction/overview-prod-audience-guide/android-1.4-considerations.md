---
description: 要最有效地使用TVSDK，您应考虑其操作的某些详细信息并遵循某些最佳实践。
seo-description: 要最有效地使用TVSDK，您应考虑其操作的某些详细信息并遵循某些最佳实践。
seo-title: 注意事项和最佳实践
title: 注意事项和最佳实践
uuid: e698ae09-280b-4406-a9b8-4f468b7a6b9c
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 注意事项和最佳实践{#considerations-and-best-practices}

要最有效地使用TVSDK，您应考虑其操作的某些详细信息并遵循某些最佳实践。

## 注意事项 {#section_tvsdk_considerations}

使用TVSDK时，请记住以下信息：

* Adobe Primetime目前不支持Android模拟器。

   您必须使用真正的设备进行测试。
* 仅HTTP实时流(HLS)内容支持播放。
* 主视频内容可以被多路复用，其中视频和音频流位于同一再现中，或者非多路复用，其中视频和音频流位于单独的再现中。
* TVSDK API是在Java中实现的。
* 当前，您需要在UI线程（即主Android线程）上运行大多数TVSDK API操作。

   在主线程上正确运行的操作可能会引发错误，并在后台线程上运行时退出。
* 视频回放需要Adobe视频引擎(AVE)。 这会影响访问媒体资源的方式和时间：

   * 在AVE提供的范围内支持隐藏式字幕。
   * 根据编码器精度，实际编码媒体持续时间可能与流资源清单中记录的持续时间不同。

      在理想的虚拟时间线和实际播放时间线之间重新同步没有可靠的方法。 用于广告管理和视频分析的流播放的进度跟踪必须使用实际的播放时间，因此报告和用户界面行为可能无法精确跟踪媒体和广告内容。
   * 从此平台上的TVSDK发出的所有媒体请求的传入用户代理名称将分配以下字符串模式：

      ```
      "Adobe Primetime/ + 
      <varname>
      originalUserAgent
      </varname>" 
      ```

      如果您在设置广告插入元数据时设置了所有广告相关调用，则使用Android默认用户代理或自定义用户代理。

## 最佳实践 {#section_tvsdk_best_practices}

以下是TVSDK的建议实践：

* 将HLS版本3.0或更高版本用于程序内容。
* 在主(UI)线程（而非后台线程）中运行大多数TVSDK操作。
