---
title: 基于时间的规则概述
description: 基于时间的规则概述
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# 基于时间的规则{#time-based-rules}

Primetime DRM对基于时间的许可限制采取“软强制”措施。 如果在视频播放期间某个时间权限过期，则Primetime DRM的默认行为是在下次重新创建视频流之前（通过调用`Netstream.stop()`和`Netstream.play()`）不限制播放。

虽然软强制是默认行为，但您也可以通过执行下列任务之一启用硬强制：

* 让您的视频播放器定期轮询许可，以确保没有任何时间限制过期。 可通过调用`DRMManager.loadVoucher(LOCAL_ONLY).`来完成此操作。错误代码指示本地存储的许可证不再有效。
* 每当用户单击&#x200B;**[!UICONTROL Pause]**&#x200B;时，您都可以录制当前视频时间戳，然后调用`Netstream.stop()`。 当用户单击“播放”按钮时，您可以搜索录制的位置，然后调用`Netstream.play()`。