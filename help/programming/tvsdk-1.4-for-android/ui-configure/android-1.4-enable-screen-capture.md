---
keywords: setSecure；VideoEngineView
title: 启用屏幕捕获
description: 启用屏幕捕获
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---

# 启用屏幕捕获{#enable-screen-capture}

默认情况下，TVSDK不允许屏幕捕获。 播放器调用 `setSecure(true)` 在 `com.adobe.ave.VideoEngineView` 构建时的对象。 您有权访问此对象，因为您必须构建 `VideoEngineView` 物件并供应给 `VideoEngine` 对象。

要在应用程序中启用屏幕捕获，请执行以下操作：

1. 构建 `com.adobe.ave.VideoEngineView` 对象。
1. 调用 `setSecure(false)` 在您的 `VideoEngineView` 对象。
