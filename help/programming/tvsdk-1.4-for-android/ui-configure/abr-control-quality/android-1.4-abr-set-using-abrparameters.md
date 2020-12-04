---
description: 您只能使用ABRControlParameters设置ABR控制值，但可以随时构造新值。
seo-description: 您只能使用ABRControlParameters设置ABR控制值，但可以随时构造新值。
seo-title: 使用ABRControlParameters配置自适应比特率
title: 使用ABRControlParameters配置自适应比特率
uuid: c877c5cc-ad72-46dc-afc4-d41ee097a9a4
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---


# 使用ABRControlParameters{#configure-adaptive-bit-rates-using-abrcontrolparameters}配置自适应比特率

您只能使用ABRControlParameters设置ABR控制值，但可以随时构造新值。

以下条件适用于`ABRControlParameters`:

* 必须在构造时为所有参数提供值。
* 在构建时间后，不能更改单个值。
* 如果指定的参数超出允许的范围，则引发`ArgumentError`。

1. 确定初始、最小和最大比特率。
1. 确定ABR策略：

   * `ABR_CONSERVATIVE`
   * `ABR_MODERATE`
   * `ABR_AGGRESSIVE`

1. 在`ABRControlParameters`构造函数中设置ABR参数值，并将它们分配给Media Player。

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

