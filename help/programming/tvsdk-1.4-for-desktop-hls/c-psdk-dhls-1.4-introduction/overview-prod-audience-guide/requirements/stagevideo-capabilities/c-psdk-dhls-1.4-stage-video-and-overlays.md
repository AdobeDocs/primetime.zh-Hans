---
description: 可将HTML叠加与StageVideo一起使用，以在Flash显示列表视频平面中显示UI元素。 此平面位于StageVideo平面上方，因此StageVideo始终显示在任何Flash显示列表元素的后面。
seo-description: 可将HTML叠加与StageVideo一起使用，以在Flash显示列表视频平面中显示UI元素。 此平面位于StageVideo平面上方，因此StageVideo始终显示在任何Flash显示列表元素的后面。
seo-title: StageVideo和HTML叠加
title: StageVideo和HTML叠加
uuid: 84e862ab-4c35-47a2-9c4e-f792d3ef5363
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# StageVideo和HTML叠加{#stagevideo-and-html-overlays}

可将HTML叠加与StageVideo一起使用，以在Flash显示列表视频平面中显示UI元素。 此平面位于StageVideo平面上方，因此StageVideo始终显示在任何Flash显示列表元素的后面。

HTML叠加是UI元素，您可以在Flash显示平面中显示在视频上，该视频由 `StageVideo` 它自己的平面呈现。 在Flash 15之前，当硬件加速不可用时，您无法使用HTML叠加。 从Flash 15开始，HTML叠加在回退到软 `StageVideo` 件渲染时显示。

>[!IMPORTANT]
>
>根据系统功能，在使用HTML叠加时，性能可能会降低到更大程度或更低程度。

请考虑以下信息：

* 在Flash Player 15中：

   * 无论硬件加速是否可用，您都可以使用HTML叠加。
   * 要使用HTML叠加，请 `wmode` 设置 `opaque`为。

* 在Flash Player 14中：

   * 当硬件加速可用时， `StageVideo` 它位于Flash显示列表下方，因此您可以使用HTML叠加。
   * 当硬件加速不可用时，视频会呈现在浏览器中所有其他元素的上方，这会阻止使用HTML叠加。

以下是将HTML叠加与以下内容结合使用的浏览器最低要求 `StageVideo`:

* Firefox版本4及更高版本
* Safari版本4及更高版本
* Internet Explorer:

   * Windows 7及更高版本上的9+版
   * Windows XP上的10+版

* Chrome版本26及更高版本

   >[!IMPORTANT]
   >
   >Windows XP和Windows Vista上不支持Chrome Pepper。

