---
description: 可以从QOSProvider类读取播放、缓冲和设备统计信息。
seo-description: 可以从QOSProvider类读取播放、缓冲和设备统计信息。
seo-title: 读取QOS播放、缓冲和设备统计信息
title: 读取QOS播放、缓冲和设备统计信息
uuid: 5ee631fc-cd6f-4f35-8621-2ffdc51a57c7
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 读取QOS播放、缓冲和设备统计信息{#read-qos-playback-buffering-and-device-statistics}

可以从QOSProvider类读取播放、缓冲和设备统计信息。

该 `QOSProvider` 类提供各种统计信息，包括有关缓冲、位速率、帧速率、时间数据等的信息。

它还提供有关设备的信息，如制造商、型号、操作系统、SDK版本和屏幕大小／密度。

1. 实例化媒体播放器。
1. 创建一 `QOSProvider` 个对象并将其附加到媒体播放器。

   ```
   // Create Media Player. 
   _mediaQosProvider = new QOSProvider; 
   _mediaQosProvider.attachMediaPlayer(_mediaPlayer);
   ```

1. （可选）阅读播放统计信息。

   读取播放统计数据的一个解决方案是具有计时器，该计时器定期从中获取新的QoS值 `QOSProvider`。 例如：

   ```
   var qosTimer:Timer = new Timer(1000); // every 1 second  
   qosTimer.addEventListener(TimerEvent.Timer, onQoSTimer);  
   qosTimer.start(); 
   private function onQoSTimer(event:TimerEvent):void { 
       var playbackInformation:PlaybackInformation = _mediaQosProvider.getPlaybackInformation(); 
       qosInfo["Frame rate"] = playbackInformation.frameRate.toFixed();  
       qosInfo["Dropped frames"] = playbackInformation.droppedFrameCount.toFixed(); 
       qosInfo["Bitrate"] = playbackInformation.bitrate.toFixed(); 
       qosInfo["Bandwidth"] = playbackInformation.perceivedBandwidth; 
       qosInfo["Buffering time"] = playbackInformation.bufferingTime.toFixed(); 
       qosInfo["Buffer length"] = playbackInformation.bufferLength.toFixed();  
       qosInfo["Buffer time"] = playbackInformation.bufferTime.toFixed(); 
       qosInfo["Empty buffer count"] = playbackInformation.emptyBufferCount.toFixed();  
       qosInfo["Time to load"] = playbackInformation.timeToLoad.toFixed();  
       qosInfo["Time to start"] = playbackInformation.timeToStart.toFixed(); 
       qosView.update(qosInfo); 
   }
   ```

1. （可选）阅读设备特定信息。

   ```
   // Show device information 
   var deviceInfo:DeviceInformation = new QOSProvider.deviceInformation; 
   qosInfo["deviceModel"] = deviceInfo.manufacturer +"-" + deviceInfo.model; 
   qosInfo["os"] = deviceInfo.os;  
   qosInfo["runtime"] = deviceInfo.runtimeVersion;  
   qosInfo["widthPixels"] = deviceInfo.widthPixels;  
   qosInfo["heightPixels"] = deviceInfo.heightPixels; 
   qosView.update(qosInfo); 
   ```

