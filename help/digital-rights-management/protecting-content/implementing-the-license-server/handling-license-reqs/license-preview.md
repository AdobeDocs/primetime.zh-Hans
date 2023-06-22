---
title: 许可证预览
description: 许可证预览
copied-description: true
exl-id: 7e6b1062-7240-4dae-86bb-bd26e7be1f14
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# 许可证预览{#license-preview}

客户端可以发送许可证预览请求，这意味着应用程序可以在请求用户购买内容之前执行预览操作，以确定用户的机器是否实际满足播放所需的所有条件。

*`License preview`* 是指客户预览许可证的能力（查看许可证允许哪些权利），而不是预览内容（在决定购买之前查看一小部分内容）的能力。 每台计算机特有的某些参数包括：可用输出及其保护状态、可用运行时/DRM版本以及DRM客户端安全级别。 许可证预览模式允许运行时/DRM客户端测试许可证服务器业务逻辑并向用户提供信息，以便他能够做出明智的决策。 因此，客户端可以看到有效的许可证是什么样的，但实际上不会收到用于解密内容的密钥。 许可证预览支持是可选的，并且仅在您实施使用此功能的自定义客户端时才需要。

要确定客户端是发送预览请求还是许可证获取请求，请调用 `LicenseRequestMessage.getRequestPhase()`并将其与 `LicenseRequestMessage.RequestPhase.Acquire`
