---
description: 您只能使用ABRControlParameters设置ABR控制值，但可以随时构造新值。
seo-description: 您只能使用ABRControlParameters设置ABR控制值，但可以随时构造新值。
seo-title: 使用ABRControlParameters配置自适应比特率
title: 使用ABRControlParameters配置自适应比特率
uuid: 283ccd3d-535b-43ca-8ca5-82d12df31798
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---


# 使用ABRControlParameters {#configure-adaptive-bit-rates-using-abrcontrolparameters}配置自适应比特率

您只能使用ABRControlParameters设置ABR控制值，但可以随时构造新值。

以下条件适用于`ABRControlParameters`:

* 在构造时，必须为所有参数提供值。
* 在构建之后，您无法更改单个值。
* 如果指定的参数超出允许的范围，则引发`ArgumentError`。

1. 确定初始、最小和最大比特率。
1. 确定ABR策略：

   * `ABR_CONSERVATIVE`
   * `ABR_MODERATE`
   * `ABR_AGGRESSIVE`

1. 在`ABRControlParameters`构造函数中设置ABR参数值，并将这些值分配给媒体播放器。

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
