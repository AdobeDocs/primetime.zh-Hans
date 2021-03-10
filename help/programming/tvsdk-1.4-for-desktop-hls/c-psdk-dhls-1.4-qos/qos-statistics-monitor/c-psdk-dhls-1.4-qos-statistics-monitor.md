---
description: 服务质量(QoS)将详细视图优惠到视频引擎的性能。 TVSDK提供有关播放、缓冲和设备的详细统计信息。
title: 服务质量统计
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---


# 服务质量统计{#quality-of-service-statistics}

服务质量(QoS)将详细视图优惠到视频引擎的性能。 TVSDK提供有关播放、缓冲和设备的详细统计信息。

TVSDK还提供有关以下下载资源的信息：

* 播放列表/清单文件
* 文件片段
* 文件的跟踪信息

## 使用加载信息{#track-at-the-fragment-level-using-load-information}在片段级别跟踪

您可以从LoadInformation类读取有关下载资源（如片段和轨道）的服务质量(QoS)信息。

1. 实现`onLoadInformationAvailable`回调事件侦听器。

   ```
   private function onLoadInformationAvailable(event:LoadInformationEvent):void { 
       var loadInformation:LoadInformation = event.loadInformation; 
       // process the load information here     
   }
   ```

1. 注册事件侦听器，TVSDK每次下载片段时都会调用它。

   ```
   player.addEventListener(LoadInformationEvent.LOAD_INFORMATION_AVAILABLE,  
                                    onLoadInformationAvailable);
   ```

1. 从传递到回调的`LoadInformation`中读取感兴趣的数据。

   <table id="table_75E61A2EB25E435DB631166A7FF64757"> 
   <thead> 
   <tr> 
      <th colname="col01" class="entry"> 属性 </th> 
      <th colname="col1" class="entry"> 类型 </th> 
      <th colname="col2" class="entry"> 说明 </th> 
   </tr> 
   </thead>
   <tbody> 
   <tr> 
      <td colname="col01"> <span class="codeph"> downloadDuration  </span> </td> 
      <td colname="col1"> <p>数字 </p> </td> 
      <td colname="col2"> <p>下载的持续时间（以毫秒为单位）。 </p> <p>TVSDK并不区分客户端连接到服务器的时间和下载完整片段所花费的时间。 例如，如果10 MB区段需要8秒钟才能下载，则TVSDK会提供该信息，但不会告诉您直到第一个字节之前需要4秒，下载整个片段还需要4秒。 </p> </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> mediaDuration  </span> </td> 
      <td colname="col1"> <p>数字 </p> </td> 
      <td colname="col2"> 已下载片段的媒体持续时间（以毫秒为单位）。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> 大小  </span> </td> 
      <td colname="col1"> <p>数字 </p> </td> 
      <td colname="col2"> 已下载资源的大小（以字节为单位）。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackIndex  </span> </td> 
      <td colname="col1"> <p>int </p> </td> 
      <td colname="col2"> 相应轨道的索引（如果已知）；否则，为0。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackName  </span> </td> 
      <td colname="col1"> <p>字符串 </p> </td> 
      <td colname="col2"> 相应轨道的名称（如果已知）；否则，为null。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackType  </span> </td> 
      <td colname="col1"> <p>字符串 </p> </td> 
      <td colname="col2"> 相应轨道的类型（如果已知）；否则，为null。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> 类型  </span> </td> 
      <td colname="col1"> <p>字符串 </p> </td> 
      <td colname="col2"> TVSDK下载的内容。 以下任一： 
      <ul id="ul_FA02F42D109344F4866073908CA4E835"> 
      <li id="li_0E2D3EBCAB58477FB5EA526C54FACFFB">MANIFEST — 播放列表/清单 </li> 
      <li id="li_D7894C2F0CB64C909C6398288EA5683A">片段 — 片段 </li> 
      <li id="li_4D4FEDB7704C411B80891B5028B0C20E">TRACK — 与特定轨道关联的片段 </li> 
      </ul> 有时，可能无法检测资源的类型。 如果发生这种情况，则返回FILE。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> url  </span> </td> 
      <td colname="col1"> <p>字符串 </p> </td> 
      <td colname="col2"> 指向已下载资源的URL。 </td> 
   </tr> 
   </tbody> 
   </table>

## 读取QOS播放、缓冲和设备统计数据{#read-qos-playback-buffering-and-device-statistics}

您可以从QOSProvider类读取播放、缓冲和设备统计信息。

`QOSProvider`类提供各种统计信息，包括有关缓冲、比特率、帧速率、时间数据等的信息。

它还提供有关设备的信息，例如制造商、型号、操作系统、SDK版本和屏幕大小/密度。

1. 实例化媒体播放器。
1. 创建一个`QOSProvider`对象，并将其连接到媒体播放器。

   ```
   // Create Media Player. 
   _mediaQosProvider = new QOSProvider; 
   _mediaQosProvider.attachMediaPlayer(_mediaPlayer);
   ```

1. （可选）阅读播放统计信息。

   读取播放统计信息的一个解决方案是设置一个计时器，该计时器从`QOSProvider`中定期获取新的QoS值。 例如：

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
