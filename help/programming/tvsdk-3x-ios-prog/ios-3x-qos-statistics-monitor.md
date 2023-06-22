---
description: 服务质量(QoS)提供了有关视频引擎执行情况的详细视图。 TVSDK提供有关播放、缓冲和设备的详细统计信息。
title: 服务质量统计数据
exl-id: 1e9f32fb-3faf-4646-8af1-0c1cc441cb42
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# 服务质量统计数据 {#quality-of-service-statistics}

服务质量(QoS)提供了有关视频引擎执行情况的详细视图。 TVSDK提供有关播放、缓冲和设备的详细统计信息。

## 读取QOS播放、缓冲和设备统计信息 {#section_9996406E2D814FA382B77E3041CB02BC}

您可以从中读取播放、缓冲和设备统计信息 `PTQOSProvider` 类。

此 `PTQOSProvider` 类提供了各种统计信息，包括有关缓冲、比特率、帧率、时间数据等的信息。

它还提供有关设备的信息，如型号、操作系统和制造商的设备ID。

>[!TIP]
>
>不能更改播放缓冲区大小，但可以监视缓冲区大小的状态以进行调试或分析。 `PTPlaybackInformation` 包括以下属性 `playbackBufferFull` 和 `playbackLikelyToKeepUp`.

1. 实例化媒体播放器。
1. 创建 `PTQOSProvider` 对象并将其附加到媒体播放器。

   此 `PTQOSProvider` 构造函数采用播放器上下文，以便可以检索特定于设备的信息。

   ```
   qosProvider = [[PTQOSProvider alloc]initWithPlayer:self.player]; 
   ```

1. （可选）读取播放统计数据。

   读取播放统计数据的一种解决方案是设置计时器，例如 `NSTimer`，定期从获取新的QoS `PTQOSProvider`. 例如：

   ```
   - (void)printPlaybackInfoLog { 
       PTPlaybackInformation *playbackInfo = qosProvider.playbackInformation;  
       if (playbackInfo) { 
           // For example: 
           NSString *infoLog = [NSString stringWithFormat:@"observedBitrate :  
                                  %f\n",playbackInfo.observedBitrate]; 
           [consoleView logMessage:@"====%@\n\n",infoLog]; 
       } 
   }
   ```

1. （可选）读取特定于设备的信息。

   ```
    PTDeviceInformation *devInfo = qosProvider.deviceInformation; 
   if (devInfo) { 
       [consoleView logMessage:@"=== qosDeviceInfo:==\n os =%@\n model =  
          %@\n id =%@\n\n", devInfo.os, devInfo.model, devInfo.id]; 
   } 
   [NSTimer scheduledTimerWithTimeInterval:2.0 target:self  
      selector:@selector(printPlaybackInfoLog) userInfo:nil repeats:YES];
   ```
