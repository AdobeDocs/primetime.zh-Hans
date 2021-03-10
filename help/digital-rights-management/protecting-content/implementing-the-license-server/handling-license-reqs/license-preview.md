---
title: 许可预览
description: 许可预览
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---


# 许可证预览{#license-preview}

客户端可以发送许可证预览请求，这意味着应用程序可以在要求用户购买内容之前执行预览操作，以确定用户的计算机是否实际满足回放所需的所有条件。

*`License preview`* 指客户预览许可（查看许可允许的权利）的能力，而不是预览内容（在决定购买之前查看内容的一小部分）。每台计算机特有的一些参数有：输出可用及其保护状态、运行时/DRM版本可用以及DRM客户端安全级别。 许可预览模式允许运行时/DRM客户端测试许可服务器业务逻辑并向用户提供信息，以便他能够做出明智的决定。 因此，客户端可以查看有效许可证的外观，但实际上不会收到用于解密内容的密钥。 支持许可证预览是可选的，并且仅当您实施使用此功能的自定义客户端时才是必需的。

要确定客户端是发送了预览请求还是许可证获取请求，请调用`LicenseRequestMessage.getRequestPhase()`并将其与`LicenseRequestMessage.RequestPhase.Acquire`进行比较
