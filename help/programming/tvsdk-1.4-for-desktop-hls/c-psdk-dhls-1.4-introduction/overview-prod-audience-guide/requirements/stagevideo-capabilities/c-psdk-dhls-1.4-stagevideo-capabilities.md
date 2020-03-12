---
description: 在支持GPU（硬件）加速的设备上，可以使用flash.media.StageVideo对象在设备硬件上处理视频。 StageVideo的可用性取决于系统不同部分的版本和功能，包括Flash Player、视频硬件、操作系统、驱动程序、浏览器、网络连接和查看上下文。
seo-description: 在支持GPU（硬件）加速的设备上，可以使用flash.media.StageVideo对象在设备硬件上处理视频。 StageVideo的可用性取决于系统不同部分的版本和功能，包括Flash Player、视频硬件、操作系统、驱动程序、浏览器、网络连接和查看上下文。
seo-title: StageVideo功能和限制
title: StageVideo功能和限制
uuid: 7556f30b-4b9f-4258-beb6-2a4ce8f05d1a
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# 概述 {#stagevideo-capabilities-and-restrictions-overview}

在支持GPU（硬件）加速的设备上，可以使用flash.media.StageVideo对象在设备硬件上处理视频。 StageVideo的可用性取决于系统不同部分的版本和功能，包括Flash Player、视频硬件、操作系统、驱动程序、浏览器、网络连接和查看上下文。

该 `StageVideo` 类允许您利用硬件加速将视频呈现在设备的最高性能级别。 可用性和性 `StageVideo` 能受以下因素影响：

* **硬件加速** -当硬件加速可用时，在设 `StageVideo` 备硬件上处理视频。 当硬件加速不可用时，响 `StageVideo` 应取决于您正在运行的Flash版本：

   * *Flash 15及更高版本* -当硬件加速不可用时， `StageVideo` 请返回软件，您无需执行任何操作。

      >[!TIP]
      >
      >当硬件加速不可用时，性能可能会显着下降。

   * *Flash 14及更早版本* -当硬件加速不可用时，将变 `StageVideo` 为不可用。 在浏览器或GPU不支持硬件加速或在Flash Player中关闭的一小组配置中，使用TVSDK HLS堆栈的视频显示将失败。 在 *HDS* 管道中 `StageVideo` ，您可以从一个备用对象（如在CPU中处理视频的Video对象）切换到另一个。

* **演示文稿上下文** -在全屏查看过程中， `StageVideo` 始终可用，并且性能将处于设备上可用的最大级别。 当不全屏查看时，视频演示文稿会落在浏览器的上下文中，浏览器的设置和功能将在该上下文中使用。

* **wmode** —— 在浏览器上下文中，设置 `wmode` 对性能至关重要。 Adobe建议您继续设 `wmode` 置以确 `direct` 保在浏览器上下文中达到最佳性能。

   >[!NOTE]
   >
   >包括、和Flash在内的因 `wmode``StageVideo`素的组合导致了不同的功能和限制，具体取决于硬件运行的速度以及您使用的Flash版本。

   * *Flash 15和更高版本* - `StageVideo` 提供所有可用的 `wmode` 设置。 但是，如果设置 `wmode` 的设置不是其他设置， `direct`则性能将会较低。

   * *Flash 14及更早版本* -如果设置 `wmode` 的设置不是 `direct`，则并非所有 `StageVideo` 浏览器都可用。

