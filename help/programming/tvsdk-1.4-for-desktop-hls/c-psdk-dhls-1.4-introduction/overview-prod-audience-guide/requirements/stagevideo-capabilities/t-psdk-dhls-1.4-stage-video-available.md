---
description: 如果StageVideo不可用，且您的应用程序尝试使用StageVideo，则TVSDK不会发出错误。 您的应用程序可以通过侦听StageVideoAvailabilityEvent来确定StageVideo是否可用。
title: 检查StageVideo是否可用
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 1%

---


# 检查StageVideo是否可用{#check-whether-stagevideo-is-available}

如果StageVideo不可用，且您的应用程序尝试使用StageVideo，则TVSDK不会发出错误。 您的应用程序可以通过侦听StageVideoAvailabilityEvent来确定StageVideo是否可用。

从Flash 15和更高版本，当硬件`StageVideo`不可用时，它将回退到软件`StageVideo`。 对于Flash 14及更早版本，您可以确定`StageVideo`是否可用。 如果`StageVideo`不可用，则可以使用`StageVideoAvailabilityEvent`了解它不可用的原因。

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
