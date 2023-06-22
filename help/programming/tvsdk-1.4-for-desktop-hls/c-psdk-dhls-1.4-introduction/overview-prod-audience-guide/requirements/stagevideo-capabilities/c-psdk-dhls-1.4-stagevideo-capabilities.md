---
description: 在支持GPU（硬件）加速的设备上，您可以使用flash.media.StageVideo对象处理设备硬件上的视频。 StageVideo的可用性取决于系统不同部分的版本和功能，包括Flash Player、视频硬件、操作系统、驱动程序、浏览器、网络连接和查看上下文。
title: StageVideo功能和限制
exl-id: 228ea2d0-5950-43f5-8cfd-640d1c482b05
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# 概述 {#stagevideo-capabilities-and-restrictions-overview}

在支持GPU（硬件）加速的设备上，您可以使用flash.media.StageVideo对象处理设备硬件上的视频。 StageVideo的可用性取决于系统不同部分的版本和功能，包括Flash Player、视频硬件、操作系统、驱动程序、浏览器、网络连接和查看上下文。

此 `StageVideo` class使您可以利用硬件加速，以设备的最高性能级别呈现视频。 的可用性和性能 `StageVideo` 受以下因素影响：

* **硬件加速**  — 当硬件加速可用时， `StageVideo` 在设备硬件上处理视频。 当硬件加速不可用时， `StageVideo` 响应取决于您运行的Flash版本：

   * *Flash15及更高版本*  — 当硬件加速不可用时， `StageVideo` 退回到软件，您无需执行任何操作。

      >[!TIP]
      >
      >当硬件加速不可用时，性能可能会显着降低。

   * *Flash14及更早版本*  — 当硬件加速不可用时， `StageVideo` 将不可用。 在浏览器或GPU不支持硬件加速，或者在Flash Player中关闭的少数配置中，使用TVSDK HLS栈栈的视频显示将失败。 在 *HDS* 管道，您可以从 `StageVideo` 到CPU中处理视频的替代对象（如Video对象）。

* **演示上下文**  — 全屏查看时， `StageVideo` 始终可用，并且性能将处于设备上可用的最高级别。 当不以全屏方式查看时，视频演示文稿位于浏览器的上下文下，其中使用浏览器的设置和功能。

* **wmode**  — 在浏览器上下文中， `wmode` 设置对性能至关重要。 Adobe建议您保留 `wmode` 设置为 `direct` 以确保在浏览器上下文中获得最佳性能。

   >[!NOTE]
   >
   >这些因素包括 `wmode`， `StageVideo`和的Flash会根据硬件运行速度和使用的Flash版本而生成不同的功能和限制。

   * *Flash15及更高版本* - `StageVideo` 在所有可用项中都可用 `wmode` 设置。 但是，如果您设置 `wmode` 到设置以外的设置 `direct`，性能将会降低。

   * *Flash14及更早版本*  — 如果设置 `wmode` 到设置以外的设置 `direct`， `StageVideo` 并非在所有浏览器中都可用。
