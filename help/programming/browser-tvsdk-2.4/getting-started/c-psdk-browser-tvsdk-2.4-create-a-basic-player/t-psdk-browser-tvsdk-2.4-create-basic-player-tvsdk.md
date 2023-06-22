---
description: 完成以下步骤以使用浏览器TVSDK创建基本播放器。
title: 使用TVSDK创建基本播放器
exl-id: ea7485e0-5d15-469b-b8b6-f9604d283492
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---

# 使用TVSDK创建基本播放器{#create-a-basic-player-using-tvsdk}

完成以下步骤以使用浏览器TVSDK创建基本播放器。

1. 创建一个新目录，您可以在其中下载浏览器TVSDK的压缩文件。
1. 从Zendesk下载浏览器TVSDK，解压缩文件，并将frameworks文件夹放在新目录中。
1. 使用为代码创建简单的HTML样板 `div` 在里面。
1. 将此样板放入您在步骤1中创建的目录的HTML文件中。

   ```
   <!DOCTYPE html> 
   
   <html lang="en"> 
   <head> 
   </head> 
   <body> 
         <div id="videoDiv" width="200" height="200"> 
        <div id="video-controls"></div> 
         </div> 
   </body> 
   </html>
   ```

1. 在head部分中添加浏览器TVSDK库。

   ```js
   <script src= "frameworks/player/dash.min.js"></script> 
   <script src= "frameworks/player/primetimemain.min.js"></script> 
   <script src= "frameworks/player/swfobject.js"></script> 
   <script src= "frameworks/player/primetimeei.min.js"></script>
   ```

1. 对于body标记，添加 `onLoad` 部分。

   ```
   <body onload="startVideo()">
   ```

1. 开始实施 `startVideo` 函数。
1. 添加脚本标记并创建 `startVideo` 函数中。

   此内容应位于页面的head部分。

   ```js
   <script> 
    function startVideo(){ 
    } 
   </script>
   ```

1. 创建 `Adobe.MediaPlayer`.

   ```js
   var player = new AdobePSDK.MediaPlayer();
   ```

1. 创建 `MediaPlayerView`.

   >[!TIP]
   >
   >这就是 `div` 之前创建的变量一起使用。

   ```js
   var view = new AdobePSDK.MediaPlayerView( 
   document.getElementById("videoDiv")); 
   player.view = view;
   ```

1. 添加播放器事件侦听器。

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange);
   ```

1. 实施事件处理程序并将其放在添加事件侦听器之前。

   ```js
   var onStatusChange = function (event) { 
    console.log(event.status); 
   
    switch (event.status) { 
     case AdobePSDK.MediaPlayerStatus.IDLE: 
      console.log("Player Status: IDLE"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.INITIALIZING: 
      console.log("Player Status: INITIALIZING"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
      console.log("Player Status: INITIALIZED"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.PREPARING: 
      console.log("Player Status: PREPARING"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.PREPARED: 
      console.log("Player Status: PREPARED"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.PLAYING: 
      console.log("Player Status: PLAYING"); 
      //update UI play/pause to show pause icon 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.PAUSED: 
      console.log("Player Status: PAUSED"); 
      //update UI play/pause to show play icon & 
      //display pause icon over video 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.SEEKING: 
      console.log("Player Status: SEEKING"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.COMPLETE: 
      console.log("Player Status: COMPLETE"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.RELEASED: 
      console.log("Player Status: RELEASED"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.RELEASED: 
      console.log("Player Status: ERROR"); 
      break; 
    } 
   }; 
   ```

1. 创建 `MediaResource`，通过M3U8链接（或mpd）。

   ```js
   var resourceUrl = "https://example.com/a/yourUrl.m3u8"; 
   var resourceType = AdobePSDK.MediaResourceType.HLS; 
   var mediaResource = new AdobePSDK.MediaResource(resourceUrl, resourceType, null, false);
   ```

1. 创建一个空配置并替换资源。

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   
   player.replaceCurrentResource(mediaResource, config);
   ```

1. 当播放器处于“已初始化”状态时，调用 `prepareToPlay`.

   ```js
   case INITIALIZED: 
    player.prepareToPlay(); // <- add this line 
    break;
   ```

1. 在播放器处于PREPARED状态后，调用 `play`.

   ```js
   case PREPARED: 
    player.play(); 
    break;
   ```
