---
description: 您可以实施一个支持DVR的VOD和实时流控制栏。 DVR支持包括可搜索窗口和客户端活动点的概念。
title: 构建增强的DVR控制栏
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---

# 构建增强的DVR控制栏 {#construct-a-control-bar-enhanced-for-dvr}

您可以实施一个支持DVR的VOD和实时流控制栏。 DVR支持包括可搜索窗口和客户端活动点的概念。

* 对于VOD，可搜索窗口的长度是整个资源的持续时间。
* 对于实时流，DVR（可搜索）窗口的长度定义为从实时播放窗口开始并在客户端实时点结束的时间范围。

  请记住以下信息：

   * 客户端活动点通过从活动窗口末尾减去缓冲的长度来计算。

     目标持续时间是一个值，大于或等于清单中片段的最大持续时间。
   * 默认值为10000毫秒。
   * 实时播放的控制栏支持DVR，方法是在开始播放时首先在客户端实时点放置大拇指，并显示一个区域，该区域标记了不允许搜寻的区域。

<!--<a id="fig_37A39A28BA714BA5A2C461357ED5BD41"></a>-->

![](assets/dvr-window.PNG){width="684"}

1. 要实施支持DVR的控制栏，请执行以下步骤 [显示具有当前播放位置的搜寻拖移栏。](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/ui-configure/android-3x-ui-seek-scrub-bar-display.md) 的差异：

   * 您可以实施仅针对可搜索范围而不是播放范围映射的控制栏。

     对于搜寻的任何用户交互都可以视为在可搜寻范围内是安全的。
   * 您可以实施一个控件栏，该控件栏已映射播放范围，但也会显示可搜索范围。

     对于控件栏：

   1. 在代表播放范围的控制栏中添加叠加。
   1. 当用户开始搜寻时，使用以下方式检查所需的搜寻位置是否位于可搜索范围内 `MediaPlayer.getSeekableRange`.

      例如：

      ```java
      TimeRange seekableRange = _mediaPlayer.getSeekableRange(); 
      if (seekableRange.contains(desiredSeekPosition)) { 
          _mediaPlayer.seek(desiredPosition); 
      }
      ```

      您还可以选择使用 `MediaPlayer.LIVE_POINT` 常量。

      ```
      mediaPlayer.seek(MediaPlayer.LIVE_POINT);
      ```
