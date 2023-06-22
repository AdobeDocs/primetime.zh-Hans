---
description: 只能使用ABRControlParameters设置ABR控制值，但可以随时构造新的控制值。
title: 使用ABRControlParameters配置自适应比特率
exl-id: 787e962c-371f-4ac8-ae13-8b38a230593f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# 使用ABRControlParameters配置自适应比特率{#configure-adaptive-bit-rates-using-abrcontrolparameters}

只能使用ABRControlParameters设置ABR控制值，但可以随时构造新的控制值。

以下条件适用于 `ABRControlParameters`：

* 必须在构建时为所有参数提供值。
* 不能在构建后更改单个值。
* 如果指定的参数超出允许的范围，则 `ArgumentError` 被抛出。

1. 确定初始比特率、最小比特率和最大比特率。
1. 确定ABR策略：

   * `ABR_CONSERVATIVE`
   * `ABR_MODERATE`
   * `ABR_AGGRESSIVE`

1. 将ABR参数值设置为 `ABRControlParameters` 构造函数并将其分配给媒体播放器。

   ```java
   public ABRControlParameters(int initialBitRate, 
     int minBitRate, 
     int maxBitRate, 
     ABRControlParameters.ABRPolicy abrPolicy, 
     int minTrickPlayBitRate, 
     int maxTrickPlayBitRate, 
     int maxTrickPlayBandwidthUsage, 
     int maxPlayoutRate);
   ```
