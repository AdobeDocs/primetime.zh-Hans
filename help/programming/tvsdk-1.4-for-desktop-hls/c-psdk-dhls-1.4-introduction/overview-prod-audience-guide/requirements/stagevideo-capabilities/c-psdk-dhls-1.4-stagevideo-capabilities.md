---
description: 在支持GPU（硬件）加速的设备上，可以使用flash.media.StageVideo对象在设备硬件上处理视频。 StageVideo的可用性取决于系统不同部分的版本和功能，包括Flash Player、视频硬件、操作系统、驱动程序、浏览器、网络连接和查看上下文。
title: StageVideo功能和限制
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---


# 概述{#stagevideo-capabilities-and-restrictions-overview}

在支持GPU（硬件）加速的设备上，可以使用flash.media.StageVideo对象在设备硬件上处理视频。 StageVideo的可用性取决于系统不同部分的版本和功能，包括Flash Player、视频硬件、操作系统、驱动程序、浏览器、网络连接和查看上下文。

`StageVideo`类允许您利用硬件加速将视频呈现在设备的最高性能级别。 `StageVideo`的可用性和性能受以下因素影响：

* **硬件加速**  — 当硬件加速可用时， `StageVideo` 在设备硬件上处理视频。当硬件加速不可用时，`StageVideo`响应取决于您运行的Flash版本：

   * *Flash 15及更高版本*  — 当硬件加速不可用时， `StageVideo` 退回到软件，您无需执行任何操作。

      >[!TIP]
      >
      >当硬件加速不可用时，性能可能会显着下降。

   * *Flash 14及更早版本*  — 当硬件加速不可用时，将 `StageVideo` 变得不可用。在浏览器或GPU不支持硬件加速或在Flash Player中关闭的一小组配置中，使用TVSDK HLS堆栈的视频显示将失败。 在&#x200B;*HDS*&#x200B;管道中，您可以从`StageVideo`切换到在CPU中处理视频的备用对象，如Video对象。

* **演示文稿**  — 在全屏查看过程 `StageVideo` 中，始终可用，并且性能将达到设备上可用的最高级别。当不全屏查看时，视频演示文稿位于浏览器的上下文中，其中使用了浏览器的设置和功能。

* **wmode**  — 在浏览器上下文中， `wmode` 设置对性能至关重要。Adobe建议将`wmode`设置为`direct`以确保在浏览器上下文中达到最佳性能。

   >[!NOTE]
   >
   >包括`wmode`、`StageVideo`和Flash的因素组合会导致不同的功能和限制，具体取决于硬件运行速度以及您使用的Flash版本。

   * *Flash 15及更高版本* - `StageVideo` 提供所有可用 `wmode` 设置。但是，如果将`wmode`设置为除`direct`之外的其他设置，则性能将会降低。

   * *Flash 14及更早版本*  — 如果您 `wmode` 设置的设置不是， `direct`则并非 `StageVideo` 在所有浏览器中都可用。

