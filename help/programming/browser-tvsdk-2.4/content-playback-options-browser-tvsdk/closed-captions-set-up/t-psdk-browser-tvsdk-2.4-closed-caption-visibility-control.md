---
description: 您可以控制隐藏式字幕的可见性。 当可见性打开时，将显示当前选定的轨道。
seo-description: 您可以控制隐藏式字幕的可见性。 当可见性打开时，将显示当前选定的轨道。
seo-title: 控制隐藏式字幕可见性
title: 控制隐藏式字幕可见性
uuid: b161a729-73f3-4019-a95e-013b42779842
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 控制隐藏式字幕可见性{#control-closed-caption-visibility}

您可以控制隐藏式字幕的可见性。 当可见性打开时，将显示当前选定的轨道。

>[!TIP]
>
>如果更改当前轨道，则可见性设置将保持不变。

如果播放器进入搜索模式时显示隐藏式字幕文本，则在搜索完成后，文本不再显示。 相反，几秒钟后，浏览器TVSDK会在结束搜索位置之后的视频中显示下一个隐藏字幕文本。

>[!TIP]
>
>隐藏式字幕的可见性值由和控 `MediaPlayer.VISIBLE` 制 `MediaPlayer.INVISIBLE`。

1. 使用该 `MediaPlayer.ccVisibility` 属性可访问隐藏式字幕的当前可见性设置。

