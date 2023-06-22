---
description: 隐藏式字幕和字幕有一些独特的差异，您可以通过不同的方式启用它们。
title: 字幕和隐藏式字幕的要求
exl-id: f90dcfb7-4fd2-41d5-8396-cdc827f8a8c4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# 字幕和隐藏式字幕的要求 {#requirements-for-subtitles-and-closed-captions}

隐藏式字幕和字幕有一些独特的差异，您可以通过不同的方式启用它们。

字幕流与主内容并行运行。 隐藏字幕是MPEG-2视频流数据包的一部分。

您应了解对隐藏式字幕和字幕的以下要求：

* **隐藏字幕**

   * 隐藏式字幕通常使用与音频相同的语言，并且还将背景声音表示为文本。
   * 隐藏字幕是视频传输流中MPEG-2视频流的数据包的一部分。
   * 隐藏式字幕在AV Foundation框架提供的范围内受支持。

* **字幕**

   * 字幕通常使用不同的语言，不包括背景声音。
   * 字幕位于与主内容并行运行的流中。

      此 `PTMediaPlayer` 播放主要内容和广告，其中主要内容可以是实时/线性或VOD，广告可以是前置广告、中置广告或后置广告。
   以下是iOS中对字幕的一些其他要求：

   * 对于时间戳， `X-TIMESTAMP-MAP` 值，该值在 `WebVTT` 文件，必须与视频时间戳匹配。

   * 对于系统，必须使用iOS 6.1或更高版本。


>[!IMPORTANT]
>
>字幕要求不适用于隐藏式字幕。
