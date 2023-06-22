---
description: 只能使用ABRControlParameters设置ABR控制值，但可以随时构造新的控制值。
title: 使用ABRControlParameters配置自适应比特率
exl-id: 1f8a4a97-0341-43e7-afdf-801275bc8c94
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# 使用ABRControlParameters配置自适应比特率 {#configure-adaptive-bit-rates-using-abrcontrolparameters}

只能使用ABRControlParameters设置ABR控制值，但可以随时构造新的控制值。

以下条件适用于 `ABRControlParameters`：

* 在构建时，必须提供所有参数的值。
* 构造后，不能更改单个值。
* 如果指定的参数超出允许的范围，则 `ArgumentError` 被抛出。

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
