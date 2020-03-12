---
description: 完成以下步骤以使用浏览器TVSDK创建基本播放器。
seo-description: 完成以下步骤以使用浏览器TVSDK创建基本播放器。
seo-title: 使用TVSDK创建基本播放器
title: 使用TVSDK创建基本播放器
uuid: ec15cf53-197f-4190-a6b2-600a57815390
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 使用TVSDK创建基本播放器{#create-a-basic-player-using-tvsdk}

完成以下步骤以使用浏览器TVSDK创建基本播放器。

1. 创建一个新目录，在该目录中可以下载浏览器TVSDK的压缩文件。
1. 从Zendesk下载浏览器TVSDK，解压缩文件，并将frameworks文件夹放在新目录中。
1. 为包含其中的代码创建一个简单的HTML `div` 样板。
1. 将此样板文件放入在步骤1中创建的目录中的HTML文件中。

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

1. 在头部分添加浏览器TVSDK库。

   ```js
   <script src= "frameworks/player/dash.min.js"></script> 
   <script src= "frameworks/player/primetimemain.min.js"></script> 
   <script src= "frameworks/player/swfobject.js"></script> 
   <script src= "frameworks/player/primetimeei.min.js"></script>
   ```

1. 对于body标签，添加章 `onLoad` 节。

   ```
   <body onload="startVideo()">
   ```

1. 开始实现该 `startVideo` 函数。
1. 添加脚本标签并在标 `startVideo` 签中创建函数。

   这应该在页面的头部分。

   ```js
   <script> 
    function startVideo(){ 
    } 
   </script>
   ```

1. 创建 `Adobe.MediaPlayer`。

   ```js
   var player = new AdobePSDK.MediaPlayer();
   ```

1. 创建 `MediaPlayerView`。

   >[!TIP]
   >
   >这是您之前 `div` 创建的内容所在的位置。

   ```js
   var view = new AdobePSDK.MediaPlayerView( 
   document.getElementById("videoDiv")); 
   player.view = view;
   ```

1. 添加播放器事件监听器。

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange);
   ```

1. 实现事件处理函数，并将它放在add事件监听器之前。

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

1. 创建 `MediaResource`通过M3U8链接（或mpd）的链接。

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

1. 当播放器处于INITIALIZED状态时，调用 `prepareToPlay`。

   ```js
   case INITIALIZED: 
    player.prepareToPlay(); // <- add this line 
    break;
   ```

1. 播放器处于PREPARED状态后，请拨叫 `play`。

   ```js
   case PREPARED: 
    player.play(); 
    break;
   ```

