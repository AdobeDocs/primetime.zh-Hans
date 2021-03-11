---
description: TVSDK下载广告段并在设备屏幕上呈现它们。
title: 广告播放阶段
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# 广告播放阶段{#ad-playback-phase}

TVSDK下载广告段并在设备屏幕上呈现它们。

此时，TVSDK已解析广告，将其放在时间轴上并尝试在屏幕上呈现内容。

在此阶段中可能出现以下主要类别的错误：

* 连接到主机服务器时出错
* 下载清单文件时出错
* 下载媒体区段时出错

对于所有三个错误类，TVSDK将触发的事件转发到您的应用程序，包括：

* 发生故障转移时触发的通知事件。
* 用户档案因故障转移算法而发生更改时的通知事件。
* 当考虑了所有故障转移选项并且无法自动执行其他操作时触发通知事件。

   您的应用程序需要采取相应的操作。

无论是否发生错误，TVSDK都会为每个`onAdBreakStart`调用onAdBreakComplete，每个`onAdStart`调用`onAdComplete`。 但是，如果无法下载区段，则时间轴中可能会有间隙。 当间隙足够大时，播放头位置中的值和报告的广告进度可能会出现不连续。
