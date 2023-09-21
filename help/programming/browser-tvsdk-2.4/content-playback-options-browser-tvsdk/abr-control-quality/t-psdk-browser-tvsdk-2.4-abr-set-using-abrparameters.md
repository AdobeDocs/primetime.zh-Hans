---
description: 只能使用ABRControlParameters设置ABR控制值，但可以随时构造新的控制值。
title: 使用ABRControlParameters配置自适应比特率
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 0%

---

# 使用ABRControlParameters配置自适应比特率{#configure-adaptive-bit-rates-using-abrcontrolparameters}

只能使用ABRControlParameters设置ABR控制值，但可以随时构造新的控制值。

下列条件适用于 `ABRControlParameters`：

* 必须在构造时提供所有参数的值。
* 构造时间之后不能更改单个值。
* 如果指定的参数在允许的范围之外，则 `ArgumentError` 被抛出。

1. 确定ABR策略：

   * `ABRControlParameters.CONSERVATIVE_POLICY`
   * `ABRControlParameters.MODERATE_POLICY`
   * `ABRControlParameters.AGGRESSIVE_POLICY`

1. 将ABR参数值设置为 `ABRControlParameters` 构造函数并将其分配给媒体播放器。

   ```js
   var abrParams = new AdobePSDK.ABRControlParameters(); 
   abrParams.initialBitRate = nInitialBitRate; 
   abrParams.minBitRate = nMinBitRate; 
   abrParams.maxBitRate = nMaxBitRate; 
   abrParams.abrPolicy = eABRPolicy; 
   player.abrControlParameters = abrParams;
   ```
