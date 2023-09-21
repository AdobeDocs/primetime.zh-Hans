---
description: 您可以使用由ExpressPlay提供支持的Primetime DRM云为TVSDK应用程序实施多个DRM解决方案。 DRM解决方案包括Apple的FairPlay、Google的Widevine、Microsoft的PlayReady以及Primetime的Adobe访问。
title: 多DRM概述
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# 多DRM工作流 {#multi-drm-workflows}

您可以使用由ExpressPlay提供支持的Primetime DRM云为TVSDK应用程序实施多个DRM解决方案。 DRM解决方案包括Apple的FairPlay、Google的Widevine、Microsoft的PlayReady以及Primetime的Adobe访问。

## 多DRM概述 {#multi-drm-overview}

AdobeTVSDK支持使用多个DRM方案的DRM保护。 Adobe选件 *Primetime DRM云，由ExpressPlay提供支持* 在多个平台上提供视频内容的打包、许可和回放。

支持的DRM方案包括Adobe *Primetime访问* DRM (AAXS)以及各种设备上的原生DRM，包括 [维德万](https://www.widevine.com) 在Chrome和Android上， [公平游戏](https://developer.apple.com/streaming/fps/) 关于Safari和iOS，以及 [PlayReady](https://www.microsoft.com/playready/) 在Edge和XboxOne上。 请联系Adobe代表，以获取有关这些平台上当前可用的DRM方案以及未来发布的预定日期的信息。

TVSDK支持由任何使用这些协议的许可证服务器颁发的DRM许可证。 除了支持多个DRM解决方案外，Adobe还提供 *Primetime DRM云，由ExpressPlay提供支持* 作为解决方案，ExpressPlay为每个解决方案运行许可证服务器。 这可以简化您的DRM许可证颁发需求的设置和维护。

使用 *Primetime DRM云，由ExpressPlay提供支持* 要在TVSDK应用程序中实施DRM需求，您必须先获取 [ExpressPlay.com](https://www.expressplay.com) 帐户。 ExpressPlay为多种不同的DRM保护方案提供许可功能，并提供包括打包和密钥管理在内的其他服务。

您的Adobe代表将首先设置您的ExpressPlay帐户。 然后，您可以配置帐户并获取 *客户验证者* 您将用于向ExpressPlay服务器发出许可证令牌请求时。
