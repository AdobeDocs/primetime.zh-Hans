---
description: TVSDK会下载广告区段并在设备屏幕上呈现它们。
title: 广告播放阶段
exl-id: c12dcf84-0daa-4bc2-8e17-fdf47a760296
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---

# 广告播放阶段{#ad-playback-phase}

TVSDK会下载广告区段并在设备屏幕上呈现它们。

此时，TVSDK已解析广告，将其定位在时间轴上，并尝试在屏幕上呈现内容。

此阶段可能会出现以下主要错误类别：

* 连接到主机服务器时出错
* 下载清单文件时出错
* 下载媒体区段时出错

对于所有三个错误类，TVSDK都会将触发的事件转发到应用程序，包括：

* 发生故障转移时触发的通知事件。
* 由于故障转移算法而更改配置文件时的通知事件。
* 当考虑了所有故障转移选项且无法自动执行其他操作时触发的通知事件。

   您的应用程序需要采取相应的操作。

无论是否出现错误，TVSDK都会为每个调用onAdBreakComplete `onAdBreakStart` 和 `onAdComplete` 表示每 `onAdStart`. 但是，如果无法下载区段，则时间轴可能存在间隙。 当间隙足够大时，播放头位置和报告的广告进度中的值可能会显示不连续。
