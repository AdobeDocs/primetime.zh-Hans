---
description: TVSDK下载广告段并在设备的屏幕上呈现它们。
seo-description: TVSDK下载广告段并在设备的屏幕上呈现它们。
seo-title: 广告播放阶段
title: 广告播放阶段
uuid: 1bbcea08-3475-4a64-9f89-c455d5dd828e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 广告播放阶段{#ad-playback-phase}

TVSDK下载广告段并在设备的屏幕上呈现它们。

此时，TVSDK已解析广告，将其放在时间轴上，并尝试在屏幕上呈现内容。

此阶段可能会出现以下主要类别的错误：

* 连接到主机服务器时出错
* 下载清单文件时出错
* 下载媒体段时出错

对于所有三个错误类，TVSDK将触发的事件转发到您的应用程序，包括：

* 故障转移时触发的通知事件。
* 配置文件因故障转移算法而发生更改时的通知事件。
* 当已考虑所有故障转移选项且无法自动执行其他操作时，将触发通知事件。

   您的应用程序需要采取相应的操作。

无论是否发生错误，TVSDK都会为每个错误和每个错误 `onAdBreakStart` 调用 `onAdComplete` onAdBreakComplete `onAdStart`。 但是，如果无法下载区段，则时间轴中可能会有间隙。 当间隙足够大时，播放头位置和报告的广告进度中的值可能出现不连续。
