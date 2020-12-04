---
description: 隐藏式字幕和字幕有一些独特的差异，您可以通过不同的方式启用它们。
seo-description: 隐藏式字幕和字幕有一些独特的差异，您可以通过不同的方式启用它们。
seo-title: 字幕和隐藏式字幕
title: 字幕和隐藏式字幕
uuid: 91daf0be-087a-4be5-86c2-f8b83da43a8f
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# 字幕和隐藏式字幕{#requirements-for-subtitles-and-closed-captions}的要求

隐藏式字幕和字幕有一些独特的差异，您可以通过不同的方式启用它们。

子标题流与主内容并行运行。 隐藏式字幕是MPEG-2视频流的数据包的一部分。

您应当了解隐藏式字幕和字幕的以下要求：

* **隐藏式字幕**

   * 隐藏式字幕通常与音频使用相同的语言，并且也将背景音效表示为文本。
   * 隐藏式字幕是视频传输流中MPEG-2视频流的数据包的一部分。
   * 在AV Foundation框架提供的范围内支持隐藏式字幕。

* **字幕**

   * 字幕通常使用不同的语言，不包含背景音效。
   * 字幕是与主内容并行运行的流。

      `PTMediaPlayer`播放主内容和广告，其中主内容可以是实时／线性或VOD，广告可以是前置、中置或后置。
   以下是iOS中字幕的一些附加要求：

   * 对于时间戳，`X-TIMESTAMP-MAP`值（在`WebVTT`文件的标题部分中指定）必须与视频时间戳匹配。

   * 对于系统，必须使用iOS 6.1或更高版本。


>[!IMPORTANT]
>
>字幕要求不适用于隐藏式字幕。

