---
description: MediaPlayer对象封装媒体播放器的行为和功能。
seo-description: MediaPlayer对象封装媒体播放器的行为和功能。
seo-title: 设置MediaPlayer
title: 设置MediaPlayer
uuid: 2279e388-6fbc-49a2-8560-218d3d31e1d6
translation-type: tm+mt
source-git-commit: af9b865bc1627a97bf8957b5460ff9b46052a7dc

---


# 设置MediaPlayer{#set-up-the-mediaplayer}

MediaPlayer对象封装媒体播放器的行为和功能。

1. 使用以 `MediaPlayer` 下方法实例化：

   ```js
   var player = new AdobePSDK.MediaPlayer();
   ```

1. 创建实 `MediaPlayerView` 例：

   ```js
   var view = new AdobePSDK.MediaPlayerView(container);
   ```

   其中 `container` 是包含您 `div` 的目标元素 `HTMLMediaElement`。

   例如，在HTML页面上：

   ```
   <div id="videoDiv"> 
   <codeph>
     <div id="video-controls"> 
          ... custom video controls 
     </div> 
   </codeph> 
   </div>
   ```

   电话：

   ```js
   var view = new  
   <codeph>
   AdobePSDK.MediaPlayerView 
   </codeph>( 
         document.getElementById("videoDiv"));  
   ```

1. 将您的实 `MediaPlayerView` 例附加到您的 `MediaPlayer` 实例：

   ```js
   player.view = view;
   ```

1. 将自定义控件元 `div` 素附加到MediaPlayer实例。

   例如，在HTML中：

   ```
   <div id="videoDiv"> 
      <div id="video-controls"> 
         ..... custom video controls 
      </div> 
   </div>
   ```

   电话：

   ```js
   if (typeof player.getView() !== 'undefined') { 
       var view = player.view; 
       view.attachVideoControls(document.getElementById("video-controls")); 
   }
   ```

该实 `MediaPlayer` 例现已可用，并且已正确配置以在设备屏幕上显示视频内容。
