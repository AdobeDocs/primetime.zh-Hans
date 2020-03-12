---
description: 服务质量(QoS)提供了视频引擎执行情况的详细视图。 浏览器TVSDK提供有关播放、缓冲和设备的详细统计信息。
seo-description: 服务质量(QoS)提供了视频引擎执行情况的详细视图。 浏览器TVSDK提供有关播放、缓冲和设备的详细统计信息。
seo-title: 服务质量统计
title: 服务质量统计
uuid: e4bb2617-d8a7-4da7-b669-d6ffab2864bb
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 服务质量统计{#quality-of-service-statistics}

服务质量(QoS)提供了视频引擎执行情况的详细视图。 浏览器TVSDK提供有关播放、缓冲和设备的详细统计信息。

## 读取QOS播放、缓冲和设备统计信息 {#read-qos-playback-buffering-and-device-statistics}

可以从QOSProvider类读取播放、缓冲和设备统计信息。

该 `QOSProvider` 类提供各种统计信息，包括有关缓冲、位速率、帧速率、时间数据等的信息。

1. 实例化媒体播放器。
1. 创建一 `QOSProvider` 个对象并将其附加到媒体播放器。

   ```js
   // Create Media Player.qosProvider =  
         new AdobePSDK.QOSProvider(); 
   qosProvider.attachMediaPlayer(player);
   ```

1. （可选）阅读播放统计信息。

   读取播放统计数据的一个解决方案是具有计时器，该计时器定期从中获取新的QoS值 `QOSProvider`。 例如：

   ```js
   var qosTimer = (function () { 
       var ref = null, 
       qosChangeInterval = 500, // in milliseconds 
   
       startTimer = function () { 
           var playbackInformation = qosProvider.playbackInformation; 
        console.log("Frame rate", playbackInformation.frameRate); 
           console.log ("Dropped frames", playbackInformation.droppedFrameCount); 
           console.log ("Bitrate", playbackInformation.bitrate); 
           console.log ("Buffering time", playbackInformation.bufferingTime); 
           console.log ("Buffer length", playbackInformation.bufferLength); 
           console.log ("Buffer time", playbackInformation.bufferTime); 
           console.log ("Empty buffer count", playbackInformation.emptyBufferCount); 
           console.log ("Time to load", playbackInformation.timeToLoad); 
           console.log ("Time to start", playbackInformation.timeToStart); 
           ref = window.setTimeout(startTimer, qosChangeInterval); 
       }; 
   
       return { 
           start: function () { 
               if (ref !== null) { 
                   // don't start another timeout if one already exists. 
                   return; 
               } 
               startTimer(); 
           }, 
   
           stop: function () { 
               window.clearTimeout(ref); 
               ref = null; 
           } 
       };  
   })() 
   
   qosTimer.start(); 
   ```

1. （可选）阅读设备特定信息。

   ```js
   // Show device information 
   DeviceInformation deviceInfo = new QOSProvider().deviceInformation; 
   console.log("OS: "+ deviceInfo.getOS()); 
   console.log("Width: "+ deviceInfo.getWidthPixels() +  
               "Height: "+ deviceInfo.getHeightPixels() );
   ```
