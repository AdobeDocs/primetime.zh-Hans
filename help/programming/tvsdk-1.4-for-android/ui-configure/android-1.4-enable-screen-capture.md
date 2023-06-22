---
keywords: setSecure；VideoEngineView
title: 启用屏幕捕获
description: 启用屏幕捕获
copied-description: true
exl-id: 5dd1bf4e-ab50-4b57-89e4-eacc291a9fe3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---

# 启用屏幕捕获{#enable-screen-capture}

默认情况下，TVSDK不允许屏幕捕获。 播放器调用 `setSecure(true)` 在 `com.adobe.ave.VideoEngineView` 构建时的对象。 您有权访问此对象，因为您必须构建 `VideoEngineView` 对象并将其提供给 `VideoEngine` 对象。

要在应用程序中启用屏幕捕获，请执行以下操作：

1. 构建 `com.adobe.ave.VideoEngineView` 对象。
1. 调用 `setSecure(false)` 在您的 `VideoEngineView` 对象。
