---
description: 您可以将HTML叠加与StageVideo结合使用，以在Flash显示列表视频平面中显示UI元素。 此平面位于StageVideo平面上方，因此StageVideo始终显示在任何Flash显示列表元素后面。
title: StageVideo和HTML叠加图
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# StageVideo和HTML叠加图{#stagevideo-and-html-overlays}

您可以将HTML叠加与StageVideo结合使用，以在Flash显示列表视频平面中显示UI元素。 此平面位于StageVideo平面上方，因此StageVideo始终显示在任何Flash显示列表元素后面。

HTML叠加是可以在由渲染的视频的Flash显示平面中显示的UI元素 `StageVideo` 在自己的飞机上。 在Flash15之前，当硬件加速不可用时，无法使用HTML叠加。 从Flash15开始，在以下情况下显示HTML叠加： `StageVideo` 回退到软件渲染。

>[!IMPORTANT]
>
>使用HTML叠加时，性能可能会或多或少地降低，具体取决于系统的功能。

请考虑以下信息：

* 在Flash Player15中：

   * 无论硬件加速是否可用，您都可以使用HTML叠加图。
   * 要使用HTML叠加，请设置 `wmode` 到 `opaque`.

* 在Flash Player14中：

   * 当硬件加速可用时， `StageVideo` 位于“Flash显示”列表下方，因此您可以使用HTML叠加图。
   * 当硬件加速不可用时，视频将在浏览器所有其他元素之上渲染，这会阻止使用HTML叠加。

以下是使用HTML叠加的浏览器最低要求 `StageVideo`：

* Firefox版本4及更高版本
* Safari版本4及更高版本
* Internet Explorer：

   * Windows 7及更高版本上的9+
   * Windows XP上的版本10+

* Chrome版本26及更高版本

  >[!IMPORTANT]
  >
  >不支持Windows XP和Windows Vista上的Chrome Pepper。
