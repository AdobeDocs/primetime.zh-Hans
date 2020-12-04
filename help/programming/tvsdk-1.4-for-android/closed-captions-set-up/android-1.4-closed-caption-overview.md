---
description: 关闭的字幕在声音无法听到或观众听不到时，将视频的音频部分作为文本显示在屏幕上。
seo-description: 关闭的字幕在声音无法听到或观众听不到时，将视频的音频部分作为文本显示在屏幕上。
seo-title: 从可用音轨中选择当前字幕轨道
title: 从可用音轨中选择当前字幕轨道
uuid: 637a70c9-9bef-4b13-8b1f-62f22f983e80
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---


# 概述{#work-with-closed-captions}

关闭的字幕在声音无法听到或观众听不到时，将视频的音频部分作为文本显示在屏幕上。

隐藏式字幕通常与音频使用相同的语言，并且还与文本显示背景音效，但字幕通常使用不同的语言，不包含背景音效。

TVSDK支持呈现以下格式：

* 608和708关闭的字幕，作为MPEG-2视频流中的数据包在HLS上作为视频传输流的一部分传送时。
* WebVTT题注文件，它们引用自HLS规范中定义的M3U8清单文件。 它们在Primetime播放器中自动作为隐藏字幕轨道可用。

您可以：

* 选择可用字幕轨道作为当前轨道，并侦听指示其他可用轨道的事件。
* 使用`MediaPlayer`接口打开或关闭关闭的字幕（可见或不可见）。
* 选择样式选项，以指示底层视频引擎如何呈现隐藏式字幕。 使用`MediaPlayerItem`接口选择字体或字体颜色等格式。
