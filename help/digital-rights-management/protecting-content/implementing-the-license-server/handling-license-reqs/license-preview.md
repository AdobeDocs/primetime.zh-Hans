---
seo-title: 许可证预览
title: 许可证预览
uuid: 3069aa16-5bf3-4af6-801c-ad823530d7eb
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 许可证预览{#license-preview}

客户端可以发送许可证预览请求，这意味着应用程序可以在请求用户购买内容之前执行预览操作，以确定用户的计算机是否实际满足回放所需的所有条件。

*`License preview`* 指客户预览许可（查看许可允许的权限）的能力，而不是预览内容（在决定购买之前查看一小部分内容）的能力。 每台计算机特有的一些参数包括：输出可用及其保护状态、可用的运行时/DRM版本和DRM客户端安全级别。 许可预览模式允许运行时/DRM客户端测试许可服务器业务逻辑并向用户提供信息，以便他能够做出明智的决定。 因此，客户端可以看到有效许可证的外观，但实际上不会收到解密内容的密钥。 对许可证预览的支持是可选的，并且仅当您实施使用此功能的自定义客户端时才是必需的。

要确定客户端是发送预览请求还是许可证获取请求，请调 `LicenseRequestMessage.getRequestPhase()`用并将其与 `LicenseRequestMessage.RequestPhase.Acquire`
