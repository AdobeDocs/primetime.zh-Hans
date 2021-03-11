---
description: 您只能使用ABRControlParameters设置ABR控制值，但可以随时构建一个新值。
title: 使用ABRControlParameters配置自适应比特率
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 0%

---


# 使用ABRControlParameters{#configure-adaptive-bit-rates-using-abrcontrolparameters}配置自适应比特率

您只能使用ABRControlParameters设置ABR控制值，但可以随时构建一个新值。

以下条件适用于`ABRControlParameters`:

* 必须在构造时为所有参数提供值。
* 在构建时间后不能更改单个值。
* 如果您指定的参数超出允许的范围，将引发`ArgumentError`。

1. 确定ABR策略：

   * `ABRControlParameters.CONSERVATIVE_POLICY`
   * `ABRControlParameters.MODERATE_POLICY`
   * `ABRControlParameters.AGGRESSIVE_POLICY`

1. 在`ABRControlParameters`构造函数中设置ABR参数值，并将它们分配给媒体播放器。

   ```js
   var abrParams = new AdobePSDK.ABRControlParameters(); 
   abrParams.initialBitRate = nInitialBitRate; 
   abrParams.minBitRate = nMinBitRate; 
   abrParams.maxBitRate = nMaxBitRate; 
   abrParams.abrPolicy = eABRPolicy; 
   player.abrControlParameters = abrParams;
   ```

