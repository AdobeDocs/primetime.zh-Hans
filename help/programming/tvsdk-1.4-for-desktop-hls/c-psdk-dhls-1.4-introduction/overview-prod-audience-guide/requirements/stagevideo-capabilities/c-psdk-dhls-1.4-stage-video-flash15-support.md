---
description: 从Flash 15和更高版本开始，当使用StageVideo进行硬件渲染不可用时，StageVideo将无缝地回退到软件StageVideo对象。
seo-description: 从Flash 15和更高版本开始，当使用StageVideo进行硬件渲染不可用时，StageVideo将无缝地回退到软件StageVideo对象。
seo-title: Flash 15支持StageVideo
title: Flash 15支持StageVideo
uuid: 49bd8703-016e-4fda-8773-5254d4774ec6
translation-type: tm+mt
source-git-commit: fd686391df0fa711bba99bc1bc312c9ef619f184

---


# Flash 15支持StageVideo{#flash-support-for-stagevideo}

从Flash 15和更高版本开始，当使用StageVideo进行硬件渲染不可用时，StageVideo将无缝地回退到软件StageVideo对象。

请考虑以下有关Flash 15 StageVideo回退到软件的信息：

* 您的应用程序中不需要任何代码更改。
* 无需更改TVSDK。

   您无需TVSDK更新即可使用StageVideo回退到软件。
* 您的应用程序需要针对Flash 15重新编译。
* 只要这些应用程序不使用Flash Player 15中引入的任何新API，您为Flash 15重新编译的应用程序将继续与Flash 14及更早版本一起使用。

   如果您的Flash 14应用程序需要使用新的Flash 15 API，则必须动态调用API并转换为“对象”类型，这样应用程序在运行时不会在Flash Player 14中失败。

## HTML叠加 {#html-overlays}

在Flash 15和更高版本中，当硬件StageVideo不可用并回退到软件StageVideo时，您可以保持HTML叠加的无缝显示。 要启用此功能，请设置 `wmode=opaque`。

某些旧版浏览器不支持硬件加速。 有关这些要求的详细信息，请参阅 [StageVideo最低要求](../../../../../tvsdk-1.4-for-desktop-hls/c-psdk-dhls-1.4-introduction/overview-prod-audience-guide/requirements/stagevideo-capabilities/r-psdk-dhls-1.4-requirements-stage-video.md)。 设置后， `wmode=opaque`视频会使用软件StageVideo渲染，这会影响性能。 通常，设置 `wmode=direct` 会将视频直接渲染到GPU，这会带来更好的性能。 但是，此选项也会覆盖HTML叠加。
