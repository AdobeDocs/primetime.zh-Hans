---
description: 服务质量(QoS)提供了有关视频引擎执行情况的详细视图。 TVSDK提供有关播放、缓冲和设备的详细统计信息。
title: 服务质量统计数据
exl-id: ab664d75-a24f-41d6-91d7-a26ad7baab9a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# 服务质量统计数据 {#quality-of-service-statistics}

服务质量(QoS)提供了有关视频引擎执行情况的详细视图。 TVSDK提供有关播放、缓冲和设备的详细统计信息。

TVSDK还提供了有关以下已下载资源的信息：

* 播放列表/清单文件
* 文件片段
* 文件的跟踪信息

## 使用加载信息在片段级别跟踪 {#track-at-the-fragment-level-using-load-information}

您可以从LoadInformation类中读取有关已下载资源（如片段和跟踪）的服务质量(QoS)信息。

1. 实施 `onLoadInformationAvailable` 回调事件侦听器。

   ```
   private function onLoadInformationAvailable(event:LoadInformationEvent):void { 
       var loadInformation:LoadInformation = event.loadInformation; 
       // process the load information here     
   }
   ```

1. 注册事件侦听器，每次下载片段时TVSDK都会调用该侦听器。

   ```
   player.addEventListener(LoadInformationEvent.LOAD_INFORMATION_AVAILABLE,  
                                    onLoadInformationAvailable);
   ```

1. 从以下位置读取感兴趣的数据 `LoadInformation` 会传递到回调的URL。

   <table id="table_75E61A2EB25E435DB631166A7FF64757"> 
   <thead> 
   <tr> 
      <th colname="col01" class="entry"> 属性 </th> 
      <th colname="col1" class="entry"> 类型 </th> 
      <th colname="col2" class="entry"> 描述 </th> 
   </tr> 
   </thead>
   <tbody> 
   <tr> 
      <td colname="col01"> <span class="codeph"> downloadduration </span> </td> 
      <td colname="col1"> <p>数字 </p> </td> 
      <td colname="col2"> <p>下载持续时间（以毫秒为单位）。 </p> <p>TVSDK不区分客户端连接到服务器所用的时间和下载完整片段所用的时间。 例如，如果下载10 MB的片段需要8秒，TVSDK会提供该信息，但不会告诉您第一个字节之前需要4秒，而下载整个片段需要4秒。 </p> </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> mediaDuration </span> </td> 
      <td colname="col1"> <p>数字 </p> </td> 
      <td colname="col2"> 已下载片段的媒体持续时间（以毫秒为单位）。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> 大小 </span> </td> 
      <td colname="col1"> <p>数字 </p> </td> 
      <td colname="col2"> 已下载资源的大小（字节）。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackIndex </span> </td> 
      <td colname="col1"> <p>int </p> </td> 
      <td colname="col2"> 相应轨道的索引（如果已知）；否则为0。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackName </span> </td> 
      <td colname="col1"> <p>字符串 </p> </td> 
      <td colname="col2"> 相应跟踪的名称（如果已知）；否则为null。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> trackType </span> </td> 
      <td colname="col1"> <p>字符串 </p> </td> 
      <td colname="col2"> 相应跟踪的类型（如果已知）；否则为null。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> type </span> </td> 
      <td colname="col1"> <p>字符串 </p> </td> 
      <td colname="col2"> TVSDK下载了什么。 以下任一项： 
      <ul id="ul_FA02F42D109344F4866073908CA4E835"> 
      <li id="li_0E2D3EBCAB58477FB5EA526C54FACFFB">清单 — 播放列表/清单 </li> 
      <li id="li_D7894C2F0CB64C909C6398288EA5683A">片段 — 片段 </li> 
      <li id="li_4D4FEDB7704C411B80891B5028B0C20E">TRACK — 与特定跟踪关联的片段 </li> 
      </ul> 有时可能无法检测资源的类型。 如果发生这种情况，则返回FILE。 </td> 
   </tr> 
   <tr> 
      <td colname="col01"> <span class="codeph"> url </span> </td> 
      <td colname="col1"> <p>字符串 </p> </td> 
      <td colname="col2"> 指向已下载资源的URL。 </td> 
   </tr> 
   </tbody> 
   </table>

## 读取QOS播放、缓冲和设备统计信息 {#read-qos-playback-buffering-and-device-statistics}

您可以从QOSProvider类中读取播放、缓冲和设备统计信息。

此 `QOSProvider` 类提供了各种统计信息，包括有关缓冲、比特率、帧率、时间数据等的信息。

它还提供有关设备的信息，例如制造商、型号、操作系统、SDK版本和屏幕大小/密度。

1. 实例化媒体播放器。
1. 创建 `QOSProvider` 对象并将其附加到媒体播放器。

   ```
   // Create Media Player. 
   _mediaQosProvider = new QOSProvider; 
   _mediaQosProvider.attachMediaPlayer(_mediaPlayer);
   ```

1. （可选）读取播放统计数据。

   读取播放统计数据的一种解决方案是设置一个计时器，该计时器定期从以下位置提取新的QoS值： `QOSProvider`. 例如：

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

1. （可选）读取特定于设备的信息。

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
