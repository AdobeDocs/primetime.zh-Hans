---
description: 您可以控制隐藏式字幕的可见性。 当可见性打开时，将显示当前选定的轨道。
title: 控制隐藏式字幕可见性
exl-id: e74c0344-43f3-4ed7-bbf2-d89dd3df8a33
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# 控制隐藏式字幕可见性{#control-closed-caption-visibility}

您可以控制隐藏式字幕的可见性。 当可见性打开时，将显示当前选定的轨道。

>[!TIP]
>
>如果更改哪个轨道为当前轨道，可见性设置将保持不变。

如果在播放器进入搜寻模式时显示隐藏式字幕文本，则搜寻完成后不再显示文本。 相反，几秒钟后，浏览器TVSDK会在视频中在结束搜寻位置后显示下一个隐藏式字幕文本。

>[!TIP]
>
>隐藏式字幕的可见度值由以下控制 `MediaPlayer.VISIBLE` 和 `MediaPlayer.INVISIBLE`.

1. 使用 `MediaPlayer.ccVisibility` 属性，用于访问隐藏式字幕的当前可见性设置。
