---
description: 您可以控制隐藏式字幕的可见性。 当可见性打开时，将显示当前选定的轨道。
seo-description: 您可以控制隐藏式字幕的可见性。 当可见性打开时，将显示当前选定的轨道。
seo-title: 控制隐藏式字幕可见性
title: 控制隐藏式字幕可见性
uuid: b161a729-73f3-4019-a95e-013b42779842
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---


# 控制隐藏式字幕可见性{#control-closed-caption-visibility}

您可以控制隐藏式字幕的可见性。 当可见性打开时，将显示当前选定的轨道。

>[!TIP]
>
>如果更改当前轨道，则可见性设置将保持不变。

如果当播放器进入搜索模式时显示隐藏字幕文本，则在搜索完成后不再显示该文本。 相反，几秒钟后，Browser TVSDK在结束搜索位置后显示视频中的下一个隐藏字幕文本。

>[!TIP]
>
>隐藏式字幕的可见性值由`MediaPlayer.VISIBLE`和`MediaPlayer.INVISIBLE`控制。

1. 使用`MediaPlayer.ccVisibility`属性访问隐藏式字幕的当前可见性设置。

