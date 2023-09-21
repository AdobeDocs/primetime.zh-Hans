---
description: 您可以控制隐藏式字幕的可见性。 当可见性打开时，将显示当前选定的轨道。
title: 控制隐藏式字幕的可见性
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# 控制隐藏式字幕的可见性{#control-closed-caption-visibility}

您可以控制隐藏式字幕的可见性。 当可见性打开时，将显示当前选定的轨道。

>[!TIP]
>
>如果更改当前跟踪，可视性设置将保持不变。

如果在播放器进入搜寻模式时显示隐藏式字幕文本，则搜寻完成后不再显示文本。 相反，几秒后，浏览器TVSDK会在视频中在结束搜寻位置后显示下一个隐藏式字幕文本。

>[!TIP]
>
>隐藏式字幕的可见性值由以下控制 `MediaPlayer.VISIBLE` 和 `MediaPlayer.INVISIBLE`.

1. 使用 `MediaPlayer.ccVisibility` 属性，用于访问隐藏式字幕的当前可见性设置。
