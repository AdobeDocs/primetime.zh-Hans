---
description: 可将HTML叠加与StageVideo一起使用，以在Flash显示列表视频平面中显示UI元素。 此平面位于StageVideo平面之上，因此StageVideo始终显示在任何Flash显示列表元素之后。
title: StageVideo和HTML叠加
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---


# StageVideo和HTML叠加{#stagevideo-and-html-overlays}

可将HTML叠加与StageVideo一起使用，以在Flash显示列表视频平面中显示UI元素。 此平面位于StageVideo平面之上，因此StageVideo始终显示在任何Flash显示列表元素之后。

HTML叠加是UI元素，可在Flash显示平面中显示在由`StageVideo`在其自身平面上呈现的视频上。 在Flash 15之前，当硬件加速不可用时，您无法使用HTML叠加。 从Flash 15开始，当`StageVideo`回退到软件渲染时，HTML叠加将显示。

>[!IMPORTANT]
>
>使用HTML叠加时，性能可能会大大或小程度地降低，具体取决于系统的功能。

请考虑以下信息：

* 在Flash Player 15中：

   * 无论硬件加速是否可用，您都可以使用HTML叠加。
   * 要使用HTML叠加，请将`wmode`设置为`opaque`。

* 在Flash Player 14中：

   * 当硬件加速可用时，`StageVideo`位于Flash显示列表下，因此您可以使用HTML叠加。
   * 当硬件加速不可用时，视频将呈现在浏览器中所有其他元素的上方，这会阻止使用HTML叠加。

以下是将HTML叠加与`StageVideo`一起使用的最低浏览器要求：

* Firefox版本4及更高版本
* Safari版本4及更高版本
* Internet Explorer:

   * Windows 7及更高版本上的9+版
   * Windows XP上的10+版

* Chrome 26及更高版本

   >[!IMPORTANT]
   >
   >Windows XP和Windows Vista上不支持Chrome Pepper。

