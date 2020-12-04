---
description: 您可以实现一个控制栏，它支持VOD和实时流播放。 DVR支持包括可搜索窗口和客户端实时点的概念。
seo-description: 您可以实现一个控制栏，它支持VOD和实时流播放。 DVR支持包括可搜索窗口和客户端实时点的概念。
seo-title: 构建用于DVR的增强的控制条
title: 构建用于DVR的增强的控制条
uuid: 83c56def-a454-4f26-bdfc-2ef2497ef9bd
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# 构建DVR{#construct-a-control-bar-enhanced-for-dvr}增强的控制条

您可以实现一个控制栏，它支持VOD和实时流播放。 DVR支持包括可搜索窗口和客户端实时点的概念。

* 对于VOD，可搜索窗口的长度是整个资产的持续时间。
* 对于实时流，DVR（可搜索）窗口的长度定义为从实时播放窗口开始到客户端实时点结束的时间范围。

   通过从实时窗口结尾减去缓冲长度来计算客户端实时点。 目标持续时间是大于或等于清单中片段的最大持续时间的值。

   用于实时回放的控制条通过首先在开始回放时将缩略图定位在客户端实时点上并通过显示标记不允许搜索的区域来支持DVR。

对于控件栏：

1. 向控件条添加表示播放范围的叠加。

1. 当用户开始要搜索时，检查所需的搜索位置是否在可搜索范围内。
