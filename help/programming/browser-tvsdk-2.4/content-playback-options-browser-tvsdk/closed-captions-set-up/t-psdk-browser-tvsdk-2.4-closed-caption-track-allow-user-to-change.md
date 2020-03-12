---
description: 以下是用户如何选择隐藏式字幕轨道的示例。
seo-description: 以下是用户如何选择隐藏式字幕轨道的示例。
seo-title: 允许用户更改音轨
title: 允许用户更改音轨
uuid: bd3d4d20-9b52-4365-b656-83ec2a405a1c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 允许用户更改音轨{#allow-the-user-to-change-the-track}

以下是用户如何选择隐藏式字幕轨道的示例。

1. 要显示可用的隐藏式字幕轨道，请使用该 `MediaPlayerItem.closedCaptionsTracks` 属性。

   ```js
   var tracks = item.closedCaptionsTracks;
   ```

1. 要设置当前的隐藏式字幕轨道，请使用该 `MediaPlayerItem.selectClosedCaptionsTrack` 方法。
1. 在准备媒体播放器项目后，使用该方法从媒体播放器中检索该 ` MediaPlayer.  currentItem ` 项目。

   ```js
   // Select the cc track with index k. 
   var item = mediaPlayer.currentItem;     
   var tracks = item.closedCaptionsTracks; 
   
   if (k >= 0 && k < tracks.length) { 
       item.selectClosedCaptionsTrack(tracks[k]); 
   }
   ```

