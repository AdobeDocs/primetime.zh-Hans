---
description: 服务质量(QoS)提供了有关视频引擎如何执行的详细视图。 浏览器TVSDK提供有关播放、缓冲和设备的详细统计信息。
title: 服务质量统计数据
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# 服务质量统计数据{#quality-of-service-statistics}

服务质量(QoS)提供了有关视频引擎如何执行的详细视图。 浏览器TVSDK提供有关播放、缓冲和设备的详细统计信息。

## 读取QOS播放、缓冲和设备统计信息 {#read-qos-playback-buffering-and-device-statistics}

您可以从QOSProvider类中读取播放、缓冲和设备统计信息。

此 `QOSProvider` 类提供了各种统计信息，包括有关缓冲、比特率、帧速率、时间数据等的信息。

1. 实例化媒体播放器。
1. 创建 `QOSProvider` 对象并将其附加到媒体播放器。

   ```js
   // Create Media Player.qosProvider =  
         new AdobePSDK.QOSProvider(); 
   qosProvider.attachMediaPlayer(player);
   ```

1. （可选）读取播放统计数据。

   读取播放统计数据的一种解决方案是设置一个计时器，该计时器定期从以下位置获取新的QoS值： `QOSProvider`. 例如：

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

1. （可选）读取特定于设备的信息。

   ```js
   // Show device information 
   DeviceInformation deviceInfo = new QOSProvider().deviceInformation; 
   console.log("OS: "+ deviceInfo.getOS()); 
   console.log("Width: "+ deviceInfo.getWidthPixels() +  
               "Height: "+ deviceInfo.getHeightPixels() );
   ```
