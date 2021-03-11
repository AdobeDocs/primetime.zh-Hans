---
keywords: setSecure;VideoEngineView
title: 启用屏幕捕捉
description: 启用屏幕捕捉
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---


# 启用屏幕捕捉{#enable-screen-capture}

默认情况下，TVSDK不允许屏幕捕捉。 播放器在构建时对`com.adobe.ave.VideoEngineView`对象调用`setSecure(true)`。 您有权访问此对象，因为您必须构建一个`VideoEngineView`对象并将其提供给`VideoEngine`对象。

要在应用程序中启用屏幕捕捉，请执行以下操作：

1. 构造`com.adobe.ave.VideoEngineView`对象。
1. 调用`VideoEngineView`对象上的`setSecure(false)`。
