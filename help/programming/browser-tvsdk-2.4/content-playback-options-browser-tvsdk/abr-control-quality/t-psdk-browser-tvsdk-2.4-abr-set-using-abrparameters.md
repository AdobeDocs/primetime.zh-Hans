---
description: 您只能用ABRControlParameters设置ABR控制值，但可以随时构建一个新值。
seo-description: 您只能用ABRControlParameters设置ABR控制值，但可以随时构建一个新值。
seo-title: 使用ABRControlParameters配置自适应比特率
title: 使用ABRControlParameters配置自适应比特率
uuid: 99b7a463-327b-48bf-8244-e41467072b44
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 使用ABRControlParameters配置自适应比特率{#configure-adaptive-bit-rates-using-abrcontrolparameters}

您只能用ABRControlParameters设置ABR控制值，但可以随时构建一个新值。

以下条件适用于 `ABRControlParameters`:

* 必须在构造时为所有参数提供值。
* 在构建时间后，不能更改单个值。
* 如果您指定的参数超出允许的范围，则会引 `ArgumentError` 发一个参数。

1. 确定ABR策略：

   * `ABRControlParameters.CONSERVATIVE_POLICY`
   * `ABRControlParameters.MODERATE_POLICY`
   * `ABRControlParameters.AGGRESSIVE_POLICY`

1. 在构造函数中设置ABR参 `ABRControlParameters` 数值，并将其分配给Media Player。

   ```js
   var abrParams = new AdobePSDK.ABRControlParameters(); 
   abrParams.initialBitRate = nInitialBitRate; 
   abrParams.minBitRate = nMinBitRate; 
   abrParams.maxBitRate = nMaxBitRate; 
   abrParams.abrPolicy = eABRPolicy; 
   player.abrControlParameters = abrParams;
   ```

