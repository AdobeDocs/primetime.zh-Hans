---
description: 'null'
keywords: setSecure;VideoEngineView
seo-description: 'null'
seo-title: 启用屏幕捕捉
title: 启用屏幕捕捉
uuid: f3d18729-e13e-47f9-b4b8-f93a2874ef16
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 0%

---


# 启用屏幕捕捉{#enable-screen-capture}

默认情况下，TVSDK不允许屏幕捕捉。 播放器在构建时调用`com.adobe.ave.VideoEngineView`对象上的`setSecure(true)`。 您有权访问此对象，因为必须构建`VideoEngineView`对象并将其提供给`VideoEngine`对象。

要在应用程序中启用屏幕捕捉，请执行以下操作：

1. 构建`com.adobe.ave.VideoEngineView`对象。
1. 调用`VideoEngineView`对象上的`setSecure(false)`。
