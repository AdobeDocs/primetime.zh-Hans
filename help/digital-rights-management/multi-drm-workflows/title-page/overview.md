---
description: 您可以使用Primetime DRM云（由ExpressPlay提供支持）为TVSDK应用程序实施多个DRM解决方案。 DRM解决方案包括Apple的FairPlay、Google的Widevine、Microsoft的PlayReady和Adobe的Primetime Access。
seo-description: 您可以使用Primetime DRM云（由ExpressPlay提供支持）为TVSDK应用程序实施多个DRM解决方案。 DRM解决方案包括Apple的FairPlay、Google的Widevine、Microsoft的PlayReady和Adobe的Primetime Access。
seo-title: 多DRM概述
title: 多DRM概述
uuid: 1705a338-baeb-4fcd-ae16-08963da55ab8
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c

---


# 多DRM工作流 {#multi-drm-workflows}

您可以使用Primetime DRM云（由ExpressPlay提供支持）为TVSDK应用程序实施多个DRM解决方案。 DRM解决方案包括Apple的FairPlay、Google的Widevine、Microsoft的PlayReady和Adobe的Primetime Access。

## 多DRM概述 {#multi-drm-overview}

Adobe TVSDK支持使用多个DRM方案的DRM保护。 Adobe提供 *Primetime DRM Cloud，由ExpressPlay提供支持* ，以在多个平台上提供视频内容的打包、许可和回放。

支持的DRM方案包括Adobe在各种设备上的 *Primetime Access* DRM(AAX)以及Android和Android上的本机 [Widevine](https://www.widevine.com) 、FairPlayPlay（在Safari和iOS上）以及 [](https://developer.apple.com/streaming/fps/)[](https://www.microsoft.com/playready/) PlayReady Ready Edge和Xbox One上的本机DRM。 请咨询Adobe代表，了解哪些DRM方案目前在这些平台上可用以及未来发行的预定日期。

TVSDK支持由任何使用这些协议的许可证服务器颁发的DRM许可证。 除了支持多个DRM解决方案外，Adobe还提供 ** Primetime DRM Cloud，该Primetime DRM Cloud由ExpressPlay提供支持，作为ExpressPlay为每个解决方案运行许可证服务器的解决方案。 这可以简化DRM许可证发行需求的设置和维护。

要使用 *Primetime DRM Cloud(由ExpressPlay提供支持* )在TVSDK应用程序中实现您的DRM需求，您必须先获得 [ExpressPlay.com帐户](https://www.expressplay.com) 。 ExpressPlay为几种不同的DRM保护方案提供许可功能，并提供包装和密钥管理等其他服务。

您的Adobe代表将首先设置您的ExpressPlay帐户。 然后，您可以配置帐户并获取客 *户身份验证器* ，以便在向ExpressPlay服务器发出许可证令牌请求时使用这些身份验证器。