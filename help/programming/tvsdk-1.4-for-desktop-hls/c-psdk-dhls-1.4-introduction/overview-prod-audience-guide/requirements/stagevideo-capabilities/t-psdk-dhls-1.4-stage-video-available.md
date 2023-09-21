---
description: 如果StageVideo不可用，并且应用程序尝试使用StageVideo，则TVSDK不会发出错误。 您的应用程序可以通过侦听StageVideoAvailabilityEvent来确定StageVideo是否可用。
title: 检查StageVideo是否可用
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 0%

---

# 检查StageVideo是否可用{#check-whether-stagevideo-is-available}

如果StageVideo不可用，并且应用程序尝试使用StageVideo，则TVSDK不会发出错误。 您的应用程序可以通过侦听StageVideoAvailabilityEvent来确定StageVideo是否可用。

从Flash15及更高版本开始，当硬件 `StageVideo` 不可用，它将回退到软件 `StageVideo`. 对于Flash14及更早版本，您可以确定 `StageVideo` 可用。 如果 `StageVideo` 不可用，您可以使用 `StageVideoAvailabilityEvent` 以了解它不可用的原因。

1. 收听 `StageVideoAvailabilityEvent` 以确定 `StageVideo` 可用。

   例如：

   ```
   private function onStageAvailable(event:StageVideoAvailabilityEvent):void {
       if (event.availability != StageVideoAvailability.AVAILABLE) {
           // process the error scenario here
       }
   }
   ```

1. 如果 `StageVideo` 不可用，请选中 `flash.media.StageVideoAvailabilityReason`.
