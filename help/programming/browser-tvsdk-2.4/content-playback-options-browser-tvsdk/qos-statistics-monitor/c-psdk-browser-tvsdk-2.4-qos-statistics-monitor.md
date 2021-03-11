---
description: 服务质量(QoS)将详细视图优惠到视频引擎的性能。 浏览器TVSDK提供有关播放、缓冲和设备的详细统计信息。
title: 服务质量统计
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 1%

---


# 服务统计数据质量{#quality-of-service-statistics}

服务质量(QoS)将详细视图优惠到视频引擎的性能。 浏览器TVSDK提供有关播放、缓冲和设备的详细统计信息。

## 读取QOS播放、缓冲和设备统计数据{#read-qos-playback-buffering-and-device-statistics}

您可以从QOSProvider类读取播放、缓冲和设备统计信息。

`QOSProvider`类提供各种统计信息，包括有关缓冲、比特率、帧速率、时间数据等的信息。

1. 实例化媒体播放器。
1. 创建一个`QOSProvider`对象，并将其连接到媒体播放器。

   ```js
   // Create Media Player.qosProvider =  
         new AdobePSDK.QOSProvider(); 
   qosProvider.attachMediaPlayer(player);
   ```

1. （可选）阅读播放统计信息。

   读取播放统计信息的一个解决方案是设置一个计时器，该计时器从`QOSProvider`中定期获取新的QoS值。 例如：

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
