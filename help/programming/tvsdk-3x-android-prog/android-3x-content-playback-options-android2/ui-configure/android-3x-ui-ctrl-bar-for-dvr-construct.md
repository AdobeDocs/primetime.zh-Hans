---
description: 您可以实现一个控制栏，它支持VOD和实时流播放。 DVR支持包括可搜索窗口和客户端实时点的概念。
seo-description: 您可以实现一个控制栏，它支持VOD和实时流播放。 DVR支持包括可搜索窗口和客户端实时点的概念。
seo-title: 构建用于DVR的增强的控制条
title: 构建用于DVR的增强的控制条
uuid: 988dcaf5-896d-4da1-8b78-5acf5a317aa3
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---


# 构建DVR {#construct-a-control-bar-enhanced-for-dvr}的增强控件条

您可以实现一个控制栏，它支持VOD和实时流播放。 DVR支持包括可搜索窗口和客户端实时点的概念。

* 对于VOD，可搜索窗口的长度是整个资产的持续时间。
* 对于实时流，DVR（可搜索）窗口的长度定义为在实时播放窗口开始并在客户端实时点结束的时间范围。

   请记住以下信息：

   * 通过从实时窗口结尾减去缓冲长度来计算客户端实时点。

      目标持续时间是大于或等于清单中片段的最大持续时间的值。
   * 默认值为10000毫秒。
   * 用于实时回放的控制条通过首先在开始回放时将缩略图定位在客户端实时点上并通过显示标记不允许搜索的区域来支持DVR。

<!--<a id="fig_37A39A28BA714BA5A2C461357ED5BD41"></a>-->

![](assets/dvr-window.PNG){width=&quot;684&quot;}

1. 要实现具有DVR支持的控制栏，请按照[显示具有当前播放位置的搜索滑动栏中的步骤进行操作。](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/ui-configure/android-3x-ui-seek-scrub-bar-display.md) 区别如下：

   * 您可以实现一个控制栏，它只映射到可搜索范围，而不是映射到播放范围。

      任何用于搜索的用户交互都可以认为在可搜索范围内是安全的。
   * 您可以实现一个控制栏，该控制栏已映射为播放范围，但也会显示可搜索范围。

      对于控件栏：
   1. 向控件条添加表示播放范围的叠加。
   1. 当用户开始进行搜索时，使用`MediaPlayer.getSeekableRange`检查所需的搜索位置是否在可搜索范围内。

      例如：

      ```java
      TimeRange seekableRange = _mediaPlayer.getSeekableRange(); 
      if (seekableRange.contains(desiredSeekPosition)) { 
          _mediaPlayer.seek(desiredPosition); 
      }
      ```

      您还可以选择使用`MediaPlayer.LIVE_POINT`常数搜索客户端实时点。

      ```
      mediaPlayer.seek(MediaPlayer.LIVE_POINT);
      ```
