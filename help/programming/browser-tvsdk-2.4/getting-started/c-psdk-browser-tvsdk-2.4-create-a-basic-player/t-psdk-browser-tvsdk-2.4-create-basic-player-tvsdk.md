---
description: 完成以下步骤以使用浏览器TVSDK创建基本播放器。
title: 使用TVSDK创建基本播放器
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# 使用TVSDK{#create-a-basic-player-using-tvsdk}创建基本播放器

完成以下步骤以使用浏览器TVSDK创建基本播放器。

1. 创建新目录，在其中可以下载Browser TVSDK的压缩文件。
1. 从Zendesk下载浏览器TVSDK，解压缩文件，并将frameworks文件夹放在新目录中。
1. 为包含`div`的代码创建一个简单的HTML样板。
1. 将此样板文件放在步骤1中创建的目录中的HTML文件中。

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

1. 在头部分添加Browser TVSDK库。

   ```js
   <script src= "frameworks/player/dash.min.js"></script> 
   <script src= "frameworks/player/primetimemain.min.js"></script> 
   <script src= "frameworks/player/swfobject.js"></script> 
   <script src= "frameworks/player/primetimeei.min.js"></script>
   ```

1. 对于body标签，添加`onLoad`部分。

   ```
   <body onload="startVideo()">
   ```

1. 开始实现`startVideo`函数。
1. 添加一个脚本标签并在标签中创建`startVideo`函数。

   这应该在页面的头部分。

   ```js
   <script> 
    function startVideo(){ 
    } 
   </script>
   ```

1. 创建`Adobe.MediaPlayer`。

   ```js
   var player = new AdobePSDK.MediaPlayer();
   ```

1. 创建`MediaPlayerView`。

   >[!TIP]
   >
   >这是您之前创建的`div`的位置。

   ```js
   var view = new AdobePSDK.MediaPlayerView( 
   document.getElementById("videoDiv")); 
   player.view = view;
   ```

1. 添加播放器事件侦听器。

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange);
   ```

1. 实现事件处理函数并将它放在添加事件侦听器前。

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

1. 创建`MediaResource`，它通过M3U8链路（或mpd）。

   ```js
   var resourceUrl = "https://example.com/a/yourUrl.m3u8"; 
   var resourceType = AdobePSDK.MediaResourceType.HLS; 
   var mediaResource = new AdobePSDK.MediaResource(resourceUrl, resourceType, null, false);
   ```

1. 创建空配置并替换资源。

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   
   player.replaceCurrentResource(mediaResource, config);
   ```

1. 当播放器处于INITIALIZED状态时，调用`prepareToPlay`。

   ```js
   case INITIALIZED: 
    player.prepareToPlay(); // <- add this line 
    break;
   ```

1. 播放器处于PREPARED状态后，调用`play`。

   ```js
   case PREPARED: 
    player.play(); 
    break;
   ```

