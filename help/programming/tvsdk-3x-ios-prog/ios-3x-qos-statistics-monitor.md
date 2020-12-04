---
description: 服务质量(QoS)优惠视频引擎的性能的详细视图。 TVSDK提供有关播放、缓冲和设备的详细统计信息。
seo-description: 服务质量(QoS)优惠视频引擎的性能的详细视图。 TVSDK提供有关播放、缓冲和设备的详细统计信息。
seo-title: 服务质量统计
title: 服务质量统计
uuid: c08c1031-616a-4776-92e2-1c405467689b
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---


# 服务质量统计数据{#quality-of-service-statistics}

服务质量(QoS)优惠视频引擎的性能的详细视图。 TVSDK提供有关播放、缓冲和设备的详细统计信息。

## 读取QOS播放、缓冲和设备统计数据{#section_9996406E2D814FA382B77E3041CB02BC}

可以从`PTQOSProvider`类读取播放、缓冲和设备统计信息。

`PTQOSProvider`类提供各种统计信息，包括有关缓冲、比特率、帧速率、时间数据等的信息。

它还提供有关设备的信息，如型号、操作系统和制造商的设备ID。

>[!TIP]
>
>无法更改播放缓冲区大小，但可以监视缓冲区大小的状态以进行调试或分析。 `PTPlaybackInformation` 包括和等 `playbackBufferFull` 属性 `playbackLikelyToKeepUp`。

1. 实例化媒体播放器。
1. 创建`PTQOSProvider`对象，并将其连接到媒体播放器。

   `PTQOSProvider`构造函数使用播放器上下文，以便能够检索设备特定信息。

   ```
   qosProvider = [[PTQOSProvider alloc]initWithPlayer:self.player]; 
   ```

1. （可选）阅读播放统计信息。

   读取播放统计信息的一个解决方案是具有一个定时器，如从`PTQOSProvider`中定期获取新的QoS值的`NSTimer`。 例如：

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
