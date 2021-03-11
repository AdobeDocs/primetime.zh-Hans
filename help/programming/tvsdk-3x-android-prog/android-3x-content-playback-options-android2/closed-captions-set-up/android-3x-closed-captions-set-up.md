---
description: 关闭的字幕在声音无法听到或观众听不到时，将视频的音频部分显示为屏幕上的文本。
title: 使用隐藏式字幕
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# 概述{#work-with-closed-captions-overview}

关闭的字幕在声音无法听到或观众听不到时，将视频的音频部分显示为屏幕上的文本。

隐藏式字幕通常与音频使用相同的语言，并且还将背景音效显示为文本，但字幕通常使用不同的语言，并且不包括背景音效。

TVSDK支持呈现以下格式：

* 608和708关闭的字幕，作为MPEG-2视频流中的数据包在HLS上作为视频传输流的一部分传送时。
* WebVTT题注文件，它引用自HLS规范中定义的M3U8清单文件。

   这些文件在Primetime播放器中自动作为隐藏字幕轨道可用。

您可以执行以下操作：

* 选择可用字幕轨道作为当前轨道，并侦听指示其他可用轨道的事件。
* 使用`MediaPlayer`接口打开（可见）或关闭（不可见）关闭字幕。
* 选择样式选项，以指示隐藏字幕由基础视频引擎呈现的方式。

   使用`MediaPlayerItem`接口选择字体或字体颜色等格式。