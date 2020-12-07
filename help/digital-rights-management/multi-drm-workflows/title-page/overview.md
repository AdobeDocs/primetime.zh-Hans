---
description: 您可以使用Primetime DRM云（由ExpressPlay提供支持）为您的TVSDK应用程序实施多个DRM解决方案。 DRM解决方案包括苹果的FairPlay、谷歌的Widevine、微软的PlayReady以及Adobe的Primetime访问。
seo-description: 您可以使用Primetime DRM云（由ExpressPlay提供支持）为您的TVSDK应用程序实施多个DRM解决方案。 DRM解决方案包括苹果的FairPlay、谷歌的Widevine、微软的PlayReady以及Adobe的Primetime访问。
seo-title: 多DRM概述
title: 多DRM概述
uuid: 1705a338-baeb-4fcd-ae16-08963da55ab8
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---


# 多DRM工作流{#multi-drm-workflows}

您可以使用Primetime DRM云（由ExpressPlay提供支持）为您的TVSDK应用程序实施多个DRM解决方案。 DRM解决方案包括苹果的FairPlay、谷歌的Widevine、微软的PlayReady以及Adobe的Primetime访问。

## 多DRM概述{#multi-drm-overview}

AdobeTVSDK使用多个DRM方案支持DRM保护。 Adobe优惠&#x200B;*Primetime DRM Cloud，由ExpressPlay*&#x200B;提供支持，可在多个平台上打包、授权和回放您的视频内容。

支持的DRM方案包括Adobe *Primetime Access* DRM(AAXS)，以及各种设备上的本机DRM，包括Chrome和Android上的[Widevine](https://www.widevine.com)、Safari和iOS上的[FairPlay](https://developer.apple.com/streaming/fps/)和[在Edge和XboxOne上播放Ready](https://www.microsoft.com/playready/)。 请咨询Adobe代表，了解这些平台目前可用的DRM方案以及未来版本的预定日期。

TVSDK支持由使用这些协议的任何许可证服务器颁发的DRM许可证。 除了支持多个DRM解决方案外，Adobe优惠&#x200B;*Primetime DRM Cloud，由ExpressPlay*&#x200B;提供支持，作为ExpressPlay为每个解决方案运行许可证服务器的解决方案。 这可以简化DRM许可证发行需求的设置和维护。

要使用&#x200B;*Primetime DRM Cloud（由ExpressPlay*&#x200B;提供支持）在TVSDK应用程序中实现您的DRM需求，您必须先获得[ExpressPlay.com](https://www.expressplay.com)帐户。 ExpressPlay为多个不同的DRM保护方案提供许可功能，还提供包装和密钥管理等其他服务。

您的Adobe代表将首先设置您的ExpressPlay帐户。 然后，您可以配置帐户并获取&#x200B;*客户身份验证器*，在向ExpressPlay服务器发出许可证令牌请求时将使用它。