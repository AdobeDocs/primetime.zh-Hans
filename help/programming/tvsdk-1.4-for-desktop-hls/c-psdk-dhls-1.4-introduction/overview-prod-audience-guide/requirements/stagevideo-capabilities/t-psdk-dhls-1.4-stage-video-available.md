---
description: 如果StageVideo不可用，且您的应用程序尝试使用StageVideo，则TVSDK不会发出错误。 您的应用程序可以通过侦听StageVideoAvailabilityEvent来确定StageVideo是否可用。
seo-description: 如果StageVideo不可用，且您的应用程序尝试使用StageVideo，则TVSDK不会发出错误。 您的应用程序可以通过侦听StageVideoAvailabilityEvent来确定StageVideo是否可用。
seo-title: 检查StageVideo是否可用
title: 检查StageVideo是否可用
uuid: 09c39442-cb9a-4892-af99-3d3d9bf1d4a7
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 1%

---


# 检查StageVideo是否可用{#check-whether-stagevideo-is-available}

如果StageVideo不可用，且您的应用程序尝试使用StageVideo，则TVSDK不会发出错误。 您的应用程序可以通过侦听StageVideoAvailabilityEvent来确定StageVideo是否可用。

从Flash15和更高版本开始，当硬件`StageVideo`不可用时，它将回退到软件`StageVideo`。 对于Flash14及更早版本，您可以确定`StageVideo`是否可用。 如果`StageVideo`不可用，则可以使用`StageVideoAvailabilityEvent`了解它不可用的原因。

1. 侦听`StageVideoAvailabilityEvent`以确定`StageVideo`是否可用。

   例如：

   ```
   private function onStageAvailable(event:StageVideoAvailabilityEvent):void {
       if (event.availability != StageVideoAvailability.AVAILABLE) {
           // process the error scenario here
       }
   }
   ```

1. 如果`StageVideo`不可用，请检查`flash.media.StageVideoAvailabilityReason`。
