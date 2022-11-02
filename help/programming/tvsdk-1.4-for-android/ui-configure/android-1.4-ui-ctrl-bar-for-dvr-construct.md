---
description: 您可以实施支持VOD和实时流播放的DVR控制栏。 DVR支持包括可查看窗口和客户端实时点的概念。
title: 构造用于DVR的增强的控制条
exl-id: a812f2d5-f1ee-4df6-9cc7-e39f55ec26f1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# 构造用于DVR的增强的控制条{#construct-a-control-bar-enhanced-for-dvr}

您可以实施支持VOD和实时流播放的DVR控制栏。 DVR支持包括可查看窗口和客户端实时点的概念。

* 对于VOD，可搜寻窗口的长度是整个资产的持续时间。
* 对于实时流播放，DVR（可查看）窗口的长度定义为从实时播放窗口开始到客户端实时点结束的时间范围。

   通过从实时窗口结束中减去缓冲的长度来计算客户端实时点。 目标持续时间是大于或等于清单中片段的最大持续时间的值。

   默认值为10000毫秒。

   实时播放的控制栏首先在开始播放时将拇指放在客户端实时点上，并显示标记不允许搜寻的区域的区域，从而支持DVR。

<!--<a id="fig_37A39A28BA714BA5A2C461357ED5BD41"></a>-->

![](assets/dvr-window.PNG){width="684"}

1. 要实施支持DVR的控制栏，请按照显示搜寻推移栏的步骤操作，但存在一些细微差别：

   * 您可以选择实施仅映射到可搜寻范围的控制栏，而不是映射到播放范围的控制栏。 任何用于搜寻的用户交互都可被视为可搜寻范围内的安全。
   * 您可以选择实施一个控制栏，该控制栏已映射到播放范围，但也会显示可查看的范围。

      对于控制栏：
   1. 在控制栏中添加一个表示播放范围的叠加图。
   1. 当用户开始搜寻时，使用检查所需搜寻位置是否在可搜寻范围内 `MediaPlayer.getSeekableRange`.

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
