---
description: MediaPlayer对象封装媒体播放器的行为和功能。
title: 设置MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---


# 设置MediaPlayer{#set-up-the-mediaplayer}

MediaPlayer对象封装媒体播放器的行为和功能。

1. 使用以下方法实例化`MediaPlayer`:

   ```js
   var player = new AdobePSDK.MediaPlayer();
   ```

1. 创建`MediaPlayerView`实例：

   ```js
   var view = new AdobePSDK.MediaPlayerView(container);
   ```

   其中`container`是包含`HTMLMediaElement`的目标`div`元素。

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

1. 将`MediaPlayerView`实例连接到`MediaPlayer`实例：

   ```js
   player.view = view;
   ```

1. 将自定义控件`div`元素连接到MediaPlayer实例。

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

`MediaPlayer`实例现已可用，并已正确配置以在设备屏幕上显示视频内容。
