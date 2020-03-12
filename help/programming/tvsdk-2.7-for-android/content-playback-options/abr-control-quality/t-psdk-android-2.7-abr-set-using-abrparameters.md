---
description: 您只能用ABRControlParameters设置ABR控制值，但可以随时构建一个新值。
seo-description: 您只能用ABRControlParameters设置ABR控制值，但可以随时构建一个新值。
seo-title: 使用ABRControlParameters配置自适应比特率
title: 使用ABRControlParameters配置自适应比特率
uuid: 7084e954-196b-492e-846f-f8b36bed13a9
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 使用ABRControlParameters配置自适应比特率 {#configure-adaptive-bit-rates-using-abrcontrolparameters}

您只能用ABRControlParameters设置ABR控制值，但可以随时构建一个新值。

以下条件适用于 `ABRControlParameters`:

* 在构造时，必须为所有参数提供值。
* 在构建之后，您无法更改单个值。
* 如果您指定的参数超出允许的范围，则会引 `ArgumentError` 发一个参数。

1. 确定初始、最小和最大比特率。
1. 确定ABR策略：

   * `ABR_CONSERVATIVE`
   * `ABR_MODERATE`
   * `ABR_AGGRESSIVE`

1. 在构造函数中设置ABR参 `ABRControlParameters` 数值，并将这些值分配给Media Player。

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

