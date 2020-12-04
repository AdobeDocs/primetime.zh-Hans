---
description: 可将HTML叠加与StageVideo一起使用，以在Flash显示列表视频平面中显示UI元素。 此平面位于StageVideo平面之上，因此StageVideo始终显示在任何Flash显示列表元素之后。
seo-description: 可将HTML叠加与StageVideo一起使用，以在Flash显示列表视频平面中显示UI元素。 此平面位于StageVideo平面之上，因此StageVideo始终显示在任何Flash显示列表元素之后。
seo-title: StageVideo和HTML叠加
title: StageVideo和HTML叠加
uuid: 84e862ab-4c35-47a2-9c4e-f792d3ef5363
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# StageVideo和HTML叠加{#stagevideo-and-html-overlays}

可将HTML叠加与StageVideo一起使用，以在Flash显示列表视频平面中显示UI元素。 此平面位于StageVideo平面之上，因此StageVideo始终显示在任何Flash显示列表元素之后。

HTML叠加是UI元素，可在视频的Flash显示平面中显示，视频由`StageVideo`在其自己的平面上呈现。 在Flash15之前，当硬件加速不可用时，您无法使用HTML叠加。 从Flash15开始，当`StageVideo`回退到软件渲染时，HTML叠加将显示。

>[!IMPORTANT]
>
>使用HTML叠加时，性能可能会大大降低或降低，具体取决于系统的功能。

请考虑以下信息：

* Flash Player15:

   * 无论硬件加速是否可用，您都可以使用HTML叠加。
   * 要使用HTML叠加，请将`wmode`设置为`opaque`。

* Flash Player14:

   * 当硬件加速可用时，`StageVideo`位于Flash显示列表下，因此您可以使用HTML叠加。
   * 当硬件加速不可用时，视频会呈现在浏览器中所有其他元素之上，这会阻止使用HTML叠加。

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

