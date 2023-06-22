---
description: 只能使用ABRControlParameters设置ABR控制值，但可以随时构造新的控制值。
title: 使用ABRControlParameters配置自适应比特率
exl-id: 53ca8516-b449-46c8-baa9-9d0d5800b3c8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 0%

---

# 使用ABRControlParameters配置自适应比特率{#configure-adaptive-bit-rates-using-abrcontrolparameters}

只能使用ABRControlParameters设置ABR控制值，但可以随时构造新的控制值。

以下条件适用于 `ABRControlParameters`：

* 必须在构建时为所有参数提供值。
* 不能在构建后更改单个值。
* 如果指定的参数超出允许的范围，则 `ArgumentError` 被抛出。

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
