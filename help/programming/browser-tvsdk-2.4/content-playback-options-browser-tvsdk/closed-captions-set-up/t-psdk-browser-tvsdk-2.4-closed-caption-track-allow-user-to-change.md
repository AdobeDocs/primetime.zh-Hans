---
description: 下面是一个示例，说明用户如何选择隐藏字幕轨道。
title: 允许用户更改轨道
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '77'
ht-degree: 0%

---


# 允许用户更改轨道{#allow-the-user-to-change-the-track}

下面是一个示例，说明用户如何选择隐藏字幕轨道。

1. 要显示可用的隐藏字幕轨道，请使用`MediaPlayerItem.closedCaptionsTracks`属性。

   ```js
   var tracks = item.closedCaptionsTracks;
   ```

1. 要设置当前的隐藏字幕轨道，请使用`MediaPlayerItem.selectClosedCaptionsTrack`方法。
1. 准备媒体播放器项后，使用` MediaPlayer.  currentItem `方法从媒体播放器中检索它。

   ```js
   // Select the cc track with index k. 
   var item = mediaPlayer.currentItem;     
   var tracks = item.closedCaptionsTracks; 
   
   if (k >= 0 && k < tracks.length) { 
       item.selectClosedCaptionsTrack(tracks[k]); 
   }
   ```

