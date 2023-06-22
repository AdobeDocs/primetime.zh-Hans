---
description: MediaPlayer对象封装媒体播放器的行为和功能。
title: 设置MediaPlay
exl-id: f492b2bb-3280-4306-ac4b-8b8d0fd68409
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---

# 设置MediaPlay{#set-up-the-mediaplayer}

MediaPlayer对象封装媒体播放器的行为和功能。

1. 实例化 `MediaPlayer` ，如下所示：

   ```js
   var player = new AdobePSDK.MediaPlayer();
   ```

1. 创建 `MediaPlayerView` 实例：

   ```js
   var view = new AdobePSDK.MediaPlayerView(container);
   ```

   位置 `container` 是目标 `div` 包含 `HTMLMediaElement`.

   例如，在“HTML”页面上：

   ```
   <div id="videoDiv"> 
   <codeph>
     <div id="video-controls"> 
          ... custom video controls 
     </div> 
   </codeph> 
   </div>
   ```

   调用：

   ```js
   var view = new  
   <codeph>
   AdobePSDK.MediaPlayerView 
   </codeph>( 
         document.getElementById("videoDiv"));  
   ```

1. 附加 `MediaPlayerView` 实例到您的 `MediaPlayer` 实例：

   ```js
   player.view = view;
   ```

1. 附加自定义控件 `div` 元素。

   例如，在HTML中：

   ```
   <div id="videoDiv"> 
      <div id="video-controls"> 
         ..... custom video controls 
      </div> 
   </div>
   ```

   调用：

   ```js
   if (typeof player.getView() !== 'undefined') { 
       var view = player.view; 
       view.attachVideoControls(document.getElementById("video-controls")); 
   }
   ```

此 `MediaPlayer` 实例现已可用，并且已正确配置为在设备屏幕上显示视频内容。
