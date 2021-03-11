---
description: 默认情况下，在开始播放时，VOD媒体开始为0，实时媒体开始为客户端实时点(DefaultMediaPlayer.LIVE_POINT)。
title: 在特定时间输入流
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 2%

---


# 在特定时间输入流{#enter-a-stream-at-a-specific-time}

默认情况下，在开始播放时，VOD媒体开始为0，实时媒体开始为客户端实时点(DefaultMediaPlayer.LIVE_POINT)。

将位置传递到`MediaPlayer.prepareToPlay`。

TVSDK将给定位置视为资产的起点。 无需执行搜索操作。 如果位置不在可搜索范围内，则使用默认位置。

例如：

```
var seekableRange:TimeRange=_mediaPlayer.seekableRange; 
if (seekableRange.contains(desiredSeekPosition) { 
    _mediaPlayer.seek(desiredSeekPosition); 
}
```
