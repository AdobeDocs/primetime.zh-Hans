---
description: 您只能使用ABRControlParameters设置ABR控制值，但可以随时构建一个新值。
title: 使用ABRControlParameters配置自适应比特率
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---


# 使用ABRControlParameters{#configure-adaptive-bit-rates-using-abrcontrolparameters}配置自适应比特率

您只能使用ABRControlParameters设置ABR控制值，但可以随时构建一个新值。

以下条件适用于`ABRControlParameters`:

* 必须在构造时为所有参数提供值。
* 在构建时间后不能更改单个值。
* 如果您指定的参数超出允许的范围，将引发`ArgumentError`。

1. 确定初始、最小和最大比特率。
1. 确定ABR策略：

   * `ABR_CONSERVATIVE`
   * `ABR_MODERATE`
   * `ABR_AGGRESSIVE`

1. 在`ABRControlParameters`构造函数中设置ABR参数值，并将它们分配给媒体播放器。

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

