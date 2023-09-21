---
description: 设置策略是指定允许用户播放受保护视频内容的时间和方式的条件的过程。
title: 设置策略
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# 设置策略{#setting-policies}

设置策略是指定允许用户播放受保护视频内容的时间和方式的条件的过程。

策略创建作为许可证令牌请求的一部分进行。 (请参阅 [https://www.expressplay.com/developer/restapi/#widevine-license-token-request](https://www.expressplay.com/developer/restapi/#widevine-license-token-request) 例如，使用Widevine)。

一旦客户的服务器端代码确定它将颁发许可证（基于权利检查、地理位置或任何其他所需信息），则它请求令牌，并且 *在令牌中* 它指定所需的 `securityLevel`， `hdcpOutputControl`、和 `licenseDuration`. 这些是Widevine策略的客户端选项。 其他DRM解决方案提供了类似的方法，但具体细节在每种情况下都不同，并在各个工作流程中加以阐述。

>[!NOTE]
>
>Adobe提供了一个示例参考服务器，其中显示了如何实施您自己的授权服务器/店面： [参考服务器：示例ExpressPlay授权服务器(SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md)
