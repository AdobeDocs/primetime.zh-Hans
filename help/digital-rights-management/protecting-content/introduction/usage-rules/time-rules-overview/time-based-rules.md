---
seo-title: 基于时间的规则概述
title: 基于时间的规则概述
uuid: 10b7766e-3b1a-4d8a-ba15-46976aa0847d
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# 基于时间的规则 {#time-based-rules}

Primetime DRM对基于时间的许可限制使用“软执行”。 如果播放视频时，时间权限过期，则Primetime DRM的默认行为是在下次重新创建视频流之前（通过调用和）不限制播 `Netstream.stop()` 放 `Netstream.play()`。

虽然软强制是默认行为，但您也可以通过执行以下任务之一来启用硬强制：

* 让视频播放器定期轮询许可证，以确保没有任何时间限制过期。 这可以通过调用错误代 `DRMManager.loadVoucher(LOCAL_ONLY).` 码指示本地存储的许可证不再有效来实现。
* 每当用户单击时， **[!UICONTROL Pause]**&#x200B;您都可以录制当前视频时间戳，然后进行呼叫 `Netstream.stop()`。 当用户单击“播放”按钮时，您可以搜索录制的位置，然后拨叫 `Netstream.play()`。