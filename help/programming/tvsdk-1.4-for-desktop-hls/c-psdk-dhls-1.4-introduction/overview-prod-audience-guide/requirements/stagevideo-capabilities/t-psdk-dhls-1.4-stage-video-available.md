---
description: 如果StageVideo不可用，并且您的应用程序尝试使用StageVideo，则TVSDK不会发出错误。 您的应用程序可以通过侦听StageVideoAvailabilityEvent来确定StageVideo是否可用。
title: 检查StageVideo是否可用
exl-id: 24136a14-8d7d-4569-9911-fac4e2de3227
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 0%

---

# 检查StageVideo是否可用{#check-whether-stagevideo-is-available}

如果StageVideo不可用，并且您的应用程序尝试使用StageVideo，则TVSDK不会发出错误。 您的应用程序可以通过侦听StageVideoAvailabilityEvent来确定StageVideo是否可用。

从Flash15及更高版本，当使用硬件时 `StageVideo` 不可用，它将回退到软件 `StageVideo`. 对于Flash14及更早版本，您可以确定 `StageVideo` 可用。 如果 `StageVideo` 不可用，您可以使用 `StageVideoAvailabilityEvent` 了解它不可用的原因。

1. 聆听 `StageVideoAvailabilityEvent` 以确定是否 `StageVideo` 可用。

   例如：

   ```
   private function onStageAvailable(event:StageVideoAvailabilityEvent):void {
       if (event.availability != StageVideoAvailability.AVAILABLE) {
           // process the error scenario here
       }
   }
   ```

1. 如果 `StageVideo` 不可用，请选中 `flash.media.StageVideoAvailabilityReason`.
