---
description: 服务质量(QoS)提供了视频引擎执行情况的详细视图。 TVSDK提供有关播放、缓冲和设备的详细统计信息。
seo-description: 服务质量(QoS)提供了视频引擎执行情况的详细视图。 TVSDK提供有关播放、缓冲和设备的详细统计信息。
seo-title: 服务质量统计
title: 服务质量统计
uuid: 8e990461-065b-4efa-b77c-b2b832f86f7d
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# 服务质量统计 {#quality-of-service-statistics}

服务质量(QoS)提供了视频引擎执行情况的详细视图。 TVSDK提供有关播放、缓冲和设备的详细统计信息。

TVSDK还提供有关以下已下载资源的信息：

* 播放列表／清单文件
* 文件片段
* 文件跟踪信息

## 使用加载信息在片段级别跟踪 {#section_4439D91E8EDC45588EF1D7BE25697350}

您可以从类中读取有关下载资源（如片段和轨道）的服务质量(QoS)信 `LoadInformation` 息。

1. 实现和注册事 `MediaPlayerEvent.LOAD_INFORMATION_AVAILABLE` 件监听器。
1. 调 `event.getLoadInformation()` 用以从传递给回调的 `event` 参数中读取相关数据。

   >[!NOTE]
   >
   >有关更多 `LoadInformation`信息， [请参阅2.7 for Android(Java)](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/index.html) API文档。

## 读取QOS播放、缓冲和设备统计信息 {#section_D21722600F324E67A9F06234D338B243}

您可以从类中读取播放、缓冲和设备统计 `QOSProvider` 数据。

该 `QOSProvider` 类提供各种统计信息，包括有关缓冲、位速率、帧速率、时间数据等的信息。 它还提供有关设备的信息，如制造商、型号、操作系统、SDK版本、制造商的设备ID和屏幕大小／密度。

1. 实例化媒体播放器。
1. 创建一 `QOSProvider` 个对象并将其附加到媒体播放器。

   构造 `QOSProvider` 函数采用播放器上下文，以便检索设备特定信息。

   ```java
   // Create Media Player. 
   _mediaQosProvider = new QOSProvider(getActivity().getApplicationContext()); 
   _mediaQosProvider.attachMediaPlayer(_mediaPlayer);
   ```

1. （可选）阅读播放统计信息。

   读取播放统计数据的一个解决方案是具有计时器，该计时器定期从中获取新的QoS值 `QOSProvider`。

   例如：

   ```java
   _playbackClock = new Clock(PLAYBACK_CLOCK, 1000); // every 1 second 
   _playbackClockEventListener = new Clock.ClockEventListener() { 
       @Override 
       public void onTick(String name) { 
           getActivity().runOnUiThread(new Runnable() { 
               @Override 
               public void run() { 
                   PlaybackInformation playbackInformation =  
                     _mediaQosProvider.getPlaybackInformation();  
                   setQosItem("Frame rate", (int) playbackInformation.getFrameRate());  
                   setQosItem("Dropped frames", (int) playbackInformation.getDroppedFrameCount()); 
                   setQosItem("Bitrate", (int) playbackInformation.getBitrate()); 
                   setQosItem("Buffering time", (int) playbackInformation.getBufferingTime());  
                   setQosItem("Buffer length", (int) playbackInformation.getBufferLength());  
                   setQosItem("Buffer time", (int) playbackInformation.getBufferTime());  
                   setQosItem("Empty buffer count", (int) playbackInformation.getEmptyBufferCount());  
                   setQosItem("Time to load", (int) playbackInformation.getTimeToLoad());  
                   setQosItem("Time to start", (int) playbackInformation.getTimeToStart()); 
                   setQosItem("Time to prepare", (int) playbackInformation.getTimeToPrepare()); 
                   setQosItem("Perceived Bandwidth", (int) playbackInformation.getPerceivedBandwidth());   
                   playbackInformation.getPerceivedBandwidth()); 
               } 
           }); 
       }; 
   }; 
   ```

1. （可选）阅读设备特定信息。

   ```java
   // Show device information 
   DeviceInformation deviceInfo = new QOSProvider(parent.getApplicationContext()). 
                                  getDeviceInformation(); 
   tv = (TextView) view.findViewById(R.id.aboutDeviceModel); 
   tv.setText(parent.getString(R.string.aboutDeviceModel) + " " +  
     deviceInfo.getManufacturer() + " - " + deviceInfo.getModel()); 
   
   tv = (TextView) view.findViewById(R.id.aboutDeviceSoftware); 
   tv.setText(parent.getString(R.string.aboutDeviceSoftware) + " " +  
     deviceInfo.getOS() + ", SDK: " + deviceInfo.getSDK()); 
   
   tv = (TextView) view.findViewById(R.id.aboutDeviceResolutin); 
   String orientation = parent.getResources().getConfiguration().orientation ==  
     Configuration.ORIENTATION_LANDSCAPE ? "landscape" : "portrait"; 
   tv.setText(parent.getString(R.string.aboutDeviceResolution) + " " +  
     deviceInfo.getWidthPixels() + "x" + deviceInfo.getHeightPixels() +  
     " (" + orientation + ")"); 
   ```

