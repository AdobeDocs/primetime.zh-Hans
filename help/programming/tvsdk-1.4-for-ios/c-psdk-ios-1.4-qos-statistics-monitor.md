---
description: 服务质量(QoS)提供了视频引擎执行情况的详细视图。 TVSDK提供有关播放、缓冲和设备的详细统计信息。
seo-description: 服务质量(QoS)提供了视频引擎执行情况的详细视图。 TVSDK提供有关播放、缓冲和设备的详细统计信息。
seo-title: 服务质量统计
title: 服务质量统计
uuid: b74cbc94-1d69-4b4b-b969-d0e985b4762b
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 服务质量统计{#quality-of-service-statistics}

服务质量(QoS)提供了视频引擎执行情况的详细视图。 TVSDK提供有关播放、缓冲和设备的详细统计信息。

## 读取QOS播放、缓冲和设备统计信息 {#section_9996406E2D814FA382B77E3041CB02BC}

您可以从类中读取播放、缓冲和设备统计 `PTQOSProvider` 数据。

该 `PTQOSProvider` 类提供各种统计信息，包括有关缓冲、位速率、帧速率、时间数据等的信息。

它还提供有关设备的信息，如型号、操作系统和制造商的设备ID。

>[!TIP]
>
>您无法更改播放缓冲区大小，但可以监视缓冲区大小的状态以进行调试或分析。 `PTPlaybackInformation` 包括和等 `playbackBufferFull` 属性 `playbackLikelyToKeepUp`。

1. 实例化媒体播放器。
1. 创建一 `PTQOSProvider` 个对象并将其附加到媒体播放器。

   构造 `PTQOSProvider` 函数采用播放器上下文，以便检索设备特定信息。

   ```
   qosProvider = [[PTQOSProvider alloc]initWithPlayer:self.player]; 
   ```

1. （可选）阅读播放统计信息。

   读取播放统计信息的一个解决方案是具有定时器， `NSTimer`例如，从中定期获取新的QoS值的定时器 `PTQOSProvider`。 例如：

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

1. （可选）阅读设备特定信息。

   ```
    PTDeviceInformation *devInfo = qosProvider.deviceInformation; 
   if (devInfo) { 
       [consoleView logMessage:@"=== qosDeviceInfo:==\n os =%@\n model =  
          %@\n id =%@\n\n", devInfo.os, devInfo.model, devInfo.id]; 
   } 
   [NSTimer scheduledTimerWithTimeInterval:2.0 target:self  
      selector:@selector(printPlaybackInfoLog) userInfo:nil repeats:YES];
   ```

