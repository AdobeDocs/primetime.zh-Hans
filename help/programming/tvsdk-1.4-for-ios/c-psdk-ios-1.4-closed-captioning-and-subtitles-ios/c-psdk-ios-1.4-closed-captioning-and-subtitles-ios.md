---
description: 隐藏式字幕和字幕有一些独特的差异，您可以通过不同的方式启用它们。
title: 字幕和隐藏式字幕
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---


# 字幕和隐藏式字幕{#requirements-for-subtitles-and-closed-captions}的要求

隐藏式字幕和字幕有一些独特的差异，您可以通过不同的方式启用它们。

子标题流与主内容并行运行。 隐藏式字幕是MPEG-2视频流的数据包的一部分。

您应当了解隐藏式字幕和字幕的以下要求：

* **隐藏式字幕**

   * 隐藏式字幕通常与音频使用相同的语言，并且还将背景声音表示为文本。
   * 隐藏式字幕是视频传输流中MPEG-2视频流的数据包的一部分。
   * 在AV Foundation框架提供的范围内支持隐藏式字幕。

* **字幕**

   * 字幕通常使用不同的语言，不包括背景音效。
   * 字幕位于与主内容并行运行的流中。

      `PTMediaPlayer`播放主内容和广告，其中主内容可以是实时/线性或VOD，广告可以是前置、中置或后置。
   以下是iOS中字幕的一些附加要求：

   * 对于时间戳，在`WebVTT`文件的标题部分中指定的`X-TIMESTAMP-MAP`值必须与视频时间戳匹配。

   * 对于系统，必须使用iOS 6.1或更高版本。


>[!IMPORTANT]
>
>字幕要求不适用于隐藏式字幕。

