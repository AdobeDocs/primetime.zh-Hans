---
description: 为了最有效地使用TVSDK，您应考虑其操作的某些详细信息并遵循某些最佳实践。
title: 注意事项和最佳实践
exl-id: 28757b1d-8aa5-4172-91ba-6bacf7b5eb22
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# 注意事项和最佳实践{#considerations-and-best-practices}

为了最有效地使用TVSDK，您应考虑其操作的某些详细信息并遵循某些最佳实践。

## 注意事项 {#section_tvsdk_considerations}

使用TVSDK时，请记住以下信息：

* Adobe Primetime目前在Android模拟器上不起作用。

   您必须使用真实设备进行测试。
* 仅HTTP实时流(HLS)内容支持播放。
* 主视频内容可以多路复用，其中视频和音频流位于同一演绎版；也可以非多路复用，其中视频和音频流位于单独的演绎版。
* TVSDK API采用Java实现。
* 目前，您需要在用户界面线程（Android主线程）上运行大多数TVSDK API操作。

   在主线程上正确运行的操作可能会引发错误，并在后台线程上运行时退出。
* 视频播放需要Adobe视频引擎(AVE)。 这会影响访问媒体资源的方式和时间：

   * 在AVE提供的范围内支持隐藏式字幕。
   * 根据编码器精度，实际的编码媒体持续时间可能与流资源清单中记录的持续时间不同。

      没有可靠的方法可以在理想的虚拟时间轴和实际的播放时间轴之间重新同步。 广告管理和视频分析的流播放进度跟踪必须使用实际播放时间，因此报告和用户界面行为可能无法准确跟踪媒体和广告内容。
   * 来自此平台TVSDK的所有媒体请求的传入用户代理名称将分配以下字符串模式：

      ```
      "Adobe Primetime/ + 
      <varname>
      originalUserAgent
      </varname>" 
      ```

      如果在设置广告插入元数据时设置了Android默认用户代理或自定义用户代理，则所有与广告相关的调用均会使用该代理。

## 最佳实践 {#section_tvsdk_best_practices}

以下是TVSDK的建议实践：

* 对程序内容使用HLS版本3.0或更高版本。
* 在主(UI)线程中运行大多数TVSDK操作，而不是在后台线程中运行。
