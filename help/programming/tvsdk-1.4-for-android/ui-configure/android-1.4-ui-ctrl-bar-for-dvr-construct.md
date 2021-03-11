---
description: 您可以实现一个控制栏，它支持VOD和实时流播放。 DVR支持包括可搜索窗口和客户端实时点的概念。
title: 构造用于DVR的增强的控制条
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---


# 构建DVR{#construct-a-control-bar-enhanced-for-dvr}增强的控制栏

您可以实现一个控制栏，它支持VOD和实时流播放。 DVR支持包括可搜索窗口和客户端实时点的概念。

* 对于VOD，可搜索窗口的长度是整个资产的持续时间。
* 对于实时流，DVR（可搜索）窗口的长度定义为从实时播放窗口开始到客户端实时点结束的时间范围。

   通过从实时窗口端减去缓冲长度来计算客户端实时点。 目标持续时间是一个大于或等于清单中片段的最大持续时间的值。

   默认值为10000毫秒。

   用于实时回放的控制条首先在开始回放时将拇指定位在客户端实时点上，并通过显示标记不允许搜索的区域的区域来支持DVR。

<!--<a id="fig_37A39A28BA714BA5A2C461357ED5BD41"></a>-->

![](assets/dvr-window.PNG){width=&quot;684&quot;}

1. 要实现具有DVR支持的控制栏，请按照显示搜索拖拉栏的步骤操作，但有一些细微差别：

   * 您可以选择实现仅针对可搜索范围而非回放范围映射的控制栏。 任何用于搜索的用户交互都可以认为在可搜索范围内是安全的。
   * 您可以选择实现一个控制栏，该控制栏已映射为播放范围，但也会显示可搜索范围。

      对于控件栏：
   1. 向表示播放范围的控制栏添加叠加。
   1. 当用户开始进行搜索时，使用`MediaPlayer.getSeekableRange`检查所需的搜索位置是否在可搜索范围内。

      例如：

      ```java
      TimeRange seekableRange = _mediaPlayer.getSeekableRange(); 
      if (seekableRange.contains(desiredSeekPosition)) { 
          _mediaPlayer.seek(desiredPosition); 
      }
      ```

      您还可以选择使用`MediaPlayer.LIVE_POINT`常量搜索客户端活动点。

      ```
      mediaPlayer.seek(MediaPlayer.LIVE_POINT);
      ```
