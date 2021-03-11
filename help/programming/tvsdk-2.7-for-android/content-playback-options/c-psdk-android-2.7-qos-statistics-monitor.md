---
description: 服务质量(QoS)提供了视频引擎的性能的详细视图。 TVSDK提供有关播放、缓冲和设备的详细统计信息。
title: 服务质量统计
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---


# 服务质量统计{#quality-of-service-statistics}

服务质量(QoS)提供了视频引擎的性能的详细视图。 TVSDK提供有关播放、缓冲和设备的详细统计信息。

TVSDK还提供有关以下下载资源的信息：

* 播放列表/清单文件
* 文件片段
* 文件的跟踪信息

## 使用加载信息{#section_4439D91E8EDC45588EF1D7BE25697350}在片段级别跟踪

您可以从`LoadInformation`类读取有关下载资源（如片段和轨道）的服务质量(QoS)信息。

1. 实现并注册`MediaPlayerEvent.LOAD_INFORMATION_AVAILABLE`事件侦听器。
1. 调用`event.getLoadInformation()`以从传递到回调的`event`参数读取相关数据。

   >[!NOTE]
   >
   >有关`LoadInformation`的详细信息，请参阅[2.7 for Android(Java)](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/index.html) API文档。

## 读取QOS播放、缓冲和设备统计数据{#section_D21722600F324E67A9F06234D338B243}

可以从`QOSProvider`类读取播放、缓冲和设备统计信息。

`QOSProvider`类提供各种统计信息，包括有关缓冲、比特率、帧速率、时间数据等的信息。 它还提供有关设备的信息，例如制造商、型号、操作系统、SDK版本、制造商的设备ID以及屏幕大小/密度。

1. 实例化媒体播放器。
1. 创建一个`QOSProvider`对象，并将其连接到媒体播放器。

   `QOSProvider`构造函数使用播放器上下文，以便它可以检索设备特定信息。

   ```java
   // Create Media Player. 
   _mediaQosProvider = new QOSProvider(getActivity().getApplicationContext()); 
   _mediaQosProvider.attachMediaPlayer(_mediaPlayer);
   ```

1. （可选）阅读播放统计信息。

   读取播放统计信息的一个解决方案是设置一个计时器，该计时器从`QOSProvider`中定期获取新的QoS值。

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

