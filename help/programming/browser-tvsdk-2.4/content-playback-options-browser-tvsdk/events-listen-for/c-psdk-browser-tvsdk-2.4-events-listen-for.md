---
description: 来自浏览器TVSDK的事件指示播放器的状态、发生的错误、您请求的操作（如视频开始播放）的完成，或隐式发生的操作（如广告完成）。
seo-description: 来自浏览器TVSDK的事件指示播放器的状态、发生的错误、您请求的操作（如视频开始播放）的完成，或隐式发生的操作（如广告完成）。
seo-title: 聆听Primetime Player事件
title: 聆听Primetime Player事件
uuid: 7b7c28ac-22ae-46a3-bbeb-bef1b04baeb3
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# 概述{#listen-for-primetime-player-events-overview}

来自浏览器TVSDK的事件指示播放器的状态、发生的错误、您请求的操作（如视频开始播放）的完成，或隐式发生的操作（如广告完成）。

由于您的应用程序需要响应这些事件中的许多，您需要实现事件处理例程，并使用Browser TVSDK注册这些例程。 例程调用相关的浏览器TVSDK方法进行适当响应。

以下是有关事件的其他信息：

* 视频播放的实时性要求对许多浏览器TVSDK操作进行异步（非阻塞）活动。
* 浏览器TVSDK支持事件驱动的视频播放器。

   它提供与播放过程中所有重要步骤对应的事件。 您使用平台的事件机制注册这些事件，并创建事件处理函数，当这些事件发生时将调用它们。 *`Event Handlers`* 也称为回调例程或事件监听器。浏览器TVSDK提供了可供事件处理程序使用的完整方法。
* 您的应用程序通常会启动非阻塞操作，例如请求播放视频开始。

   浏览器TVSDK通过调度事件(如视频开始播放时)和事件（视频结束时）与应用程序进行异步通信。 其他事件可以指示播放器的状态更改和错误情况。 您的事件处理程序会采取适当的操作。

