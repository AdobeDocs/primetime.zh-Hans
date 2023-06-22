---
description: 从Flash15及更高版本开始，当无法使用StageVideo进行硬件渲染时，StageVideo会无缝回退到软件StageVideo对象。
title: Flash15对StageVideo的支持
exl-id: 23ef0806-3aa5-4c48-a4f7-4ad9b72bdcc9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---

# Flash15对StageVideo的支持{#flash-support-for-stagevideo}

从Flash15及更高版本开始，当无法使用StageVideo进行硬件渲染时，StageVideo会无缝回退到软件StageVideo对象。

请考虑以下有关Flash15 StageVideo回退到软件的信息：

* 您的应用程序中不需要更改代码。
* 无需对TVSDK进行更改。

   您不需要TVSDK更新即可使用StageVideo回退到软件。
* 您的应用程序需要为Flash15重新编译。
* 您为Flash15重新编译的应用程序将继续用于Flash14和更早版本，只要这些应用程序不使用Flash Player15中引入的任何新API。

   如果您的Flash14应用程序需要使用新的Flash15 API，则必须动态调用该API，并对“对象”类型进行转换，以便该应用程序在运行时不会在Flash Player14中失败。

## HTML叠加图 {#html-overlays}

在Flash15及更高版本中，您可以在硬件StageVideo不可用并回退到软件StageVideo时，保持HTML叠加的无缝显示。 要启用此功能，请设置 `wmode=opaque`.

某些旧版浏览器不支持硬件加速。 有关这些要求的详细信息，请参阅 [StageVideo最低要求](../../../../../tvsdk-1.4-for-desktop-hls/c-psdk-dhls-1.4-introduction/overview-prod-audience-guide/requirements/stagevideo-capabilities/r-psdk-dhls-1.4-requirements-stage-video.md). 当您设置时 `wmode=opaque`，则视频使用软件StageVideo渲染，这可能会影响性能。 通常，设置 `wmode=direct` 直接将视频渲染到GPU，从而极大地提高了性能。 但是，此选项也会覆盖HTML叠加图。
