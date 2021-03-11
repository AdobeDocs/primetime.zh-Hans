---
description: 您可以控制隐藏式字幕的可见性。 当可见性打开时，将显示当前选定的轨道。
title: 控制隐藏字幕可见性
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# 控制隐藏字幕可见性{#control-closed-caption-visibility}

您可以控制隐藏式字幕的可见性。 当可见性打开时，将显示当前选定的轨道。

>[!TIP]
>
>如果更改当前轨道，则可见性设置保持不变。

如果当播放器进入搜索模式时显示隐藏字幕文本，则在搜索完成后不再显示该文本。 相反，几秒钟后，Browser TVSDK在结束搜索位置后在视频中显示下一个隐藏字幕文本。

>[!TIP]
>
>隐藏式字幕的可见性值由`MediaPlayer.VISIBLE`和`MediaPlayer.INVISIBLE`控制。

1. 使用`MediaPlayer.ccVisibility`属性访问隐藏式字幕的当前可见性设置。

