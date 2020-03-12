---
description: 设置策略是指定用户何时以及如何播放受保护视频内容的条件的过程。
seo-description: 设置策略是指定用户何时以及如何播放受保护视频内容的条件的过程。
seo-title: 设置策略
title: 设置策略
uuid: 2d2672ce-5ed4-4868-aa5e-0a9e21a809b3
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 设置策略{#setting-policies}

设置策略是指定用户何时以及如何播放受保护视频内容的条件的过程。

策略创建是作为许可证令牌请求的一部分进行的。 (有关使 [用Widevine的示例](https://www.expressplay.com/developer/restapi/#widevine-license-token-request) ，请参阅https://www.expressplay.com/developer/restapi/#widevine-license-token-request)。

一旦客户的服务器端代码确定将发布许可证（基于授权检查、地理位置或任何其他必需信息），它就会请求一个令牌，并在 *令牌中指定* 、 `securityLevel`和 `hdcpOutputControl``licenseDuration`。 这些是Widevine策略的客户端选项。 其他DRM解决方案提供类似的方法，但每种情况下的详细信息都不同，并在各个工作流程中加以阐述。

>[!NOTE]
>
>Adobe提供了一个示例参考服务器，用于说明如何实现您自己的授权服务器／店面：参 [考服务器：示例ExpressPlay授权服务器(SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md)

