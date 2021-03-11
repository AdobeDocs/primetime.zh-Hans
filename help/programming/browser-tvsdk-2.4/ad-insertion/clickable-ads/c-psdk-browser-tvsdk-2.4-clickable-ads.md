---
description: 浏览器TVSDK为您的视频应用程序提供响应用户点击可点击广告所需的信息。
title: 可点击广告
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# 概述{#clickable-ads-overview}

浏览器TVSDK为您的视频应用程序提供响应用户点击可点击广告所需的信息。

当用户单击可单击的广告时，视频应用程序的典型响应是打开新的浏览器窗口并导航到与该广告关联的URL。 为便于执行此操作，Browser TVSDK将触发广告通知，您的应用程序可以使用这些通知来管理点进过程。

在您的应用程序中，您可以向用户提供在播放可单击广告时单击（例如按钮）的控件。 您需要为由与广告关联的Browser TVSDK触发的事件创建处理函数(例如，广告开始、已点击广告和完成广告)。 最后，您需要实现应用程序在用户广告点击后将遵循的特定行为（例如，是否暂停广告、显示点进URL等）。

>[!NOTE]
>
>浏览器TVSDK附带的参考播放器包括处理点进广告的一个可能的工作解决方案。