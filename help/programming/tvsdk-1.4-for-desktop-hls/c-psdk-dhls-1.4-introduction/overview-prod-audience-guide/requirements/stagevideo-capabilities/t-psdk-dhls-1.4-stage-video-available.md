---
description: 如果StageVideo不可用，且您的应用程序尝试使用StageVideo，则TVSDK不会发出错误。 您的应用程序可以通过侦听StageVideoAvailabilityEvent来确定StageVideo是否可用。
seo-description: 如果StageVideo不可用，且您的应用程序尝试使用StageVideo，则TVSDK不会发出错误。 您的应用程序可以通过侦听StageVideoAvailabilityEvent来确定StageVideo是否可用。
seo-title: 检查StageVideo是否可用
title: 检查StageVideo是否可用
uuid: 09c39442-cb9a-4892-af99-3d3d9bf1d4a7
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 检查StageVideo是否可用{#check-whether-stagevideo-is-available}

如果StageVideo不可用，且您的应用程序尝试使用StageVideo，则TVSDK不会发出错误。 您的应用程序可以通过侦听StageVideoAvailabilityEvent来确定StageVideo是否可用。

从Flash 15和更高版本开始，当 `StageVideo` 硬件不可用时，它将回归到软件 `StageVideo`。 对于Flash 14及更早版本，您可以确定是否 `StageVideo` 可用。 如果 `StageVideo` 不可用，您可以使用了解 `StageVideoAvailabilityEvent` 它不可用的原因。

1. 侦听以 `StageVideoAvailabilityEvent` 确定是否 `StageVideo` 可用。

   例如：

   ```
   private function onStageAvailable(event:StageVideoAvailabilityEvent):void {
       if (event.availability != StageVideoAvailability.AVAILABLE) {
           // process the error scenario here
       }
   }
   ```

1. 如果 `StageVideo` 不可用，请选中 `flash.media.StageVideoAvailabilityReason`。
