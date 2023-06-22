---
title: 基于时间的规则概述
description: 基于时间的规则概述
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# 基于时间的规则 {#time-based-rules}

Primetime DRM使用基于时间的许可证限制的“软实施”。 如果时间权限在视频播放期间过期，则Primetime DRM的默认行为是在下次重新创建视频流之前（通过调用）不限制播放 `Netstream.stop()` 和 `Netstream.play()`)。

虽然软实施是默认行为，但您也可以通过执行以下任务之一来启用硬实施：

* 让您的视频播放器定期轮询许可证，以确保时间限制未过期。 这可以通过调用 `DRMManager.loadVoucher(LOCAL_ONLY).` 错误代码指示本地存储的许可证不再有效。
* 每当用户单击时 **[!UICONTROL Pause]**，您可以记录当前视频时间戳，然后调用 `Netstream.stop()`. 当用户单击“播放”按钮时，您可以搜索到录制的位置，然后调用 `Netstream.play()`.