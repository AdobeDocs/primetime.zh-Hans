---
title: 网络拓扑概述
description: 网络拓扑概述
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# 概述 {#network-topology-overview}

成功部署Adobe Primetime DRM后，必须维护Primetime DRM生产服务器的安全。

>[!NOTE]
>
>Primetime DRM以前称为Adobe访问，在此之前称为Flash Access。

您可以使用 *反向代理* 确保Primetime DRM Web应用程序的不同URL集可供外部和内部用户使用。 *反向代理* 比允许用户直接连接到运行Primetime DRM的应用程序服务器更安全，并且此配置对运行Primetime DRM的应用程序服务器执行所有HTTP请求。 用户只能访问反向代理，并且只能尝试反向代理支持的URL连接。

<!--<a id="fig_8083A8C794B646CD87985EC891B60663"></a>-->

![](assets/AdobeAccess_4_SecureDeployment.png)
