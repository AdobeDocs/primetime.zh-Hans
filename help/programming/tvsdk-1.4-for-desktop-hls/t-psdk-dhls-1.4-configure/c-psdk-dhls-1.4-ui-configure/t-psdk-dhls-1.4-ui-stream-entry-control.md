---
description: 默认情况下，开始播放时，VOD媒体从0开始，实时媒体从客户端实时点(DefaultMediaPlayer.LIVE_POINT)开始。
title: 在特定时间输入流
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---

# 在特定时间输入流{#enter-a-stream-at-a-specific-time}

默认情况下，开始播放时，VOD媒体从0开始，实时媒体从客户端实时点(DefaultMediaPlayer.LIVE_POINT)开始。

将职位传递给 `MediaPlayer.prepareToPlay`.

TVSDK将给定位置视为资源的起点。 不需要搜寻操作。 如果位置不在可搜索范围内，则使用默认位置。

例如：

```
var seekableRange:TimeRange=_mediaPlayer.seekableRange; 
if (seekableRange.contains(desiredSeekPosition) { 
    _mediaPlayer.seek(desiredSeekPosition); 
}
```
