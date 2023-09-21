---
description: 以下示例介绍了用户如何选择隐藏式字幕跟踪。
title: 允许用户更改曲目
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '77'
ht-degree: 0%

---

# 允许用户更改曲目{#allow-the-user-to-change-the-track}

以下示例介绍了用户如何选择隐藏式字幕跟踪。

1. 要显示可用的隐藏式字幕轨道，请使用 `MediaPlayerItem.closedCaptionsTracks` 属性。

   ```js
   var tracks = item.closedCaptionsTracks;
   ```

1. 要设置当前的隐藏式字幕轨道，请使用 `MediaPlayerItem.selectClosedCaptionsTrack` 方法。
1. 在准备媒体播放器项目后，使用 ` MediaPlayer.  currentItem ` 方法。

   ```js
   // Select the cc track with index k. 
   var item = mediaPlayer.currentItem;     
   var tracks = item.closedCaptionsTracks; 
   
   if (k >= 0 && k < tracks.length) { 
       item.selectClosedCaptionsTrack(tracks[k]); 
   }
   ```
