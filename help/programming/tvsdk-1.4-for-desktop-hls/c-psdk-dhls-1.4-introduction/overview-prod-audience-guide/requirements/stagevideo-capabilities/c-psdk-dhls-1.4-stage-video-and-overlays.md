---
description: 您可以使用带有StageVideo的HTML叠加图在Flash显示列表视频平面中显示UI元素。 此平面位于StageVideo平面的上方，因此StageVideo始终显示在任何Flash显示列表元素的后面。
title: StageVideo和HTML叠加图
exl-id: 6beda4c8-0981-4a38-bd5e-5714b9ec7efa
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# StageVideo和HTML叠加图{#stagevideo-and-html-overlays}

您可以使用带有StageVideo的HTML叠加图在Flash显示列表视频平面中显示UI元素。 此平面位于StageVideo平面的上方，因此StageVideo始终显示在任何Flash显示列表元素的后面。

HTML叠加是UI元素，您可以在其渲染的视频的Flash显示平面中显示这些元素 `StageVideo` 自己搭的飞机。 在Flash15之前，当硬件加速不可用时，无法使用HTML叠加。 从Flash15开始，在以下情况下显示HTML叠加图： `StageVideo` 回退到软件渲染。

>[!IMPORTANT]
>
>使用HTML叠加时，性能可能会或多或少地降低，具体取决于您的系统功能。

请考虑以下信息：

* 在Flash Player15中：

   * 无论硬件加速是否可用，您都可以使用HTML叠加图。
   * 要使用HTML叠加图，请设置 `wmode` 到 `opaque`.

* 在Flash Player14中：

   * 当硬件加速可用时， `StageVideo` 位于Flash显示列表下方，因此您可以使用HTML叠加图。
   * 当硬件加速不可用时，视频将在浏览器所有其他元素之上渲染，从而阻止使用HTML叠加图。

以下是使用HTML叠加的浏览器最低要求 `StageVideo`：

* Firefox版本4及更高版本
* Safari版本4及更高版本
* Internet Explorer：

   * Windows 7及更高版本上的版本9+
   * Windows XP上的版本10+

* Chrome 26版及更高版本

   >[!IMPORTANT]
   >
   >不支持Windows XP和Windows Vista上的Chrome Pepper。
