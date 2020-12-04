---
seo-title: 基于时间的规则概述
title: 基于时间的规则概述
uuid: 10b7766e-3b1a-4d8a-ba15-46976aa0847d
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# 基于时间的规则{#time-based-rules}

Primetime DRM对基于时间的许可限制使用“软执行”。 如果播放视频期间某个时间权限过期，则Primetime DRM的默认行为是在下次重新创建视频流之前（通过调用`Netstream.stop()`和`Netstream.play()`）不限制播放。

尽管软强制是默认行为，您也可以通过执行下列任务之一启用硬强制：

* 让视频播放器定期轮询许可证以确保所有时间限制都未过期。 这可以通过调用`DRMManager.loadVoucher(LOCAL_ONLY).`来完成。错误代码指示本地存储的许可证不再有效。
* 只要用户单击&#x200B;**[!UICONTROL Pause]**，您就可以录制当前视频时间戳，然后调用`Netstream.stop()`。 当用户单击“播放”按钮时，您可以搜索录制的位置，然后调用`Netstream.play()`。