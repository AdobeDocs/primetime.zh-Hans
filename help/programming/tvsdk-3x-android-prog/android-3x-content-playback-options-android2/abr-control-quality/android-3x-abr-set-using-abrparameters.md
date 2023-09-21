---
description: 只能使用ABRControlParameters设置ABR控制值，但可以随时构造新的控制值。
title: 使用ABRControlParameters配置自适应比特率
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# 使用ABRControlParameters配置自适应比特率 {#configure-adaptive-bit-rates-using-abrcontrolparameters}

只能使用ABRControlParameters设置ABR控制值，但可以随时构造新的控制值。

下列条件适用于 `ABRControlParameters`：

* 在构建时，必须提供所有参数的值。
* 构造后，不能更改单个值。
* 如果指定的参数在允许的范围之外，则 `ArgumentError` 被抛出。

1. 确定初始、最小和最大比特率。
1. 确定ABR策略：

   * `ABR_CONSERVATIVE`
   * `ABR_MODERATE`
   * `ABR_AGGRESSIVE`

1. 将ABR参数值设置为 `ABRControlParameters` 构造函数并将值分配给媒体播放器。

   ```
   public ABRControlParameters(int initialBitRate, 
     int minBitRate, 
     int maxBitRate, 
     ABRControlParameters.ABRPolicy abrPolicy, 
     int minTrickPlayBitRate, 
     int maxTrickPlayBitRate, 
     int maxTrickPlayBandwidthUsage, 
     int maxPlayoutRate);
   ```
