---
description: 服务质量(QoS)提供了有关视频引擎如何执行的详细视图。 TVSDK提供有关播放、缓冲和设备的详细统计信息。
title: 服务质量统计数据
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# 服务质量统计数据 {#quality-of-service-statistics}

服务质量(QoS)提供了有关视频引擎如何执行的详细视图。 TVSDK提供有关播放、缓冲和设备的详细统计信息。

TVSDK还提供了有关以下已下载资源的信息：

* 播放列表/清单文件
* 文件片段
* 文件的跟踪信息

## 使用加载信息在片段级别跟踪 {#section_4439D91E8EDC45588EF1D7BE25697350}

您可以从以下位置读取有关已下载资源（如片段和轨道）的服务质量(QoS)信息： `LoadInformation` 类。

1. 实施并注册 `MediaPlayerEvent.LOAD_INFORMATION_AVAILABLE` 事件侦听器。
1. 调用 `event.getLoadInformation()` 以从 `event` 传递给回调的参数。

   >[!NOTE]
   >
   >有关的更多信息 `LoadInformation`，请参见 [3.0 for Android (Java)](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.0/index.html) API文档。

## 读取QOS播放、缓冲和设备统计信息 {#section_D21722600F324E67A9F06234D338B243}

您可以从中读取播放、缓冲和设备统计信息 `QOSProvider` 类。

此 `QOSProvider` 类提供了各种统计信息，包括有关缓冲、比特率、帧速率、时间数据等的信息。 它还提供有关设备的信息，如制造商、型号、操作系统、SDK版本、制造商的设备ID和屏幕大小/密度。

1. 实例化媒体播放器。
1. 创建 `QOSProvider` 对象并将其附加到媒体播放器。

   此 `QOSProvider` 构造函数采用播放器上下文，以便可以检索特定于设备的信息。

   ```java
   // Create Media Player. 
   _mediaQosProvider = new QOSProvider(getActivity().getApplicationContext()); 
   _mediaQosProvider.attachMediaPlayer(_mediaPlayer);
   ```

1. （可选）读取播放统计数据。

   读取播放统计数据的一种解决方案是设置一个计时器，该计时器定期从以下位置获取新的QoS值： `QOSProvider`.

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

1. （可选）读取特定于设备的信息。

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
