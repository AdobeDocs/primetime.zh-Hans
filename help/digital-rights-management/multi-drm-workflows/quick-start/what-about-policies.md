---
description: 设置策略是指定允许用户何时以及如何播放受保护视频内容的过程。
title: 设置策略
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# 设置策略{#setting-policies}

设置策略是指定允许用户何时以及如何播放受保护视频内容的过程。

策略创建作为许可证令牌请求的一部分进行。 (有关使用Widevine的示例，请参阅[https://www.expressplay.com/developer/restapi/#widevine-license-token-request](https://www.expressplay.com/developer/restapi/#widevine-license-token-request))。

一旦客户的服务器端代码确定将颁发许可证（基于授权检查、地理位置或任何其他必需信息），它就会请求令牌，并在令牌&#x200B;*中指定所需的`securityLevel`、`hdcpOutputControl`和`licenseDuration`。*&#x200B;这些是Widevine策略的客户端选项。 其他DRM解决方案也优惠了类似的方法，但每种情况下的细节都有所不同，并在各个工作流中加以阐述。

>[!NOTE]
>
>Adobe提供了一个示例参考服务器，用于说明如何实现您自己的授权服务器/店面：[参考服务器：示例ExpressPlay授权服务器(SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md)

