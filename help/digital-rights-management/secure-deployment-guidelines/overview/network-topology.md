---
title: 网络拓扑概述
description: 网络拓扑概述
copied-description: true
exl-id: a4737ea3-407a-48fd-ae3e-4df56a4c1812
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# 概述 {#network-topology-overview}

成功部署Adobe Primetime DRM后，必须维护Primetime DRM生产服务器的安全性。

>[!NOTE]
>
>Primetime DRM以前称为Adobe访问，之前称为Flash Access。

您可以使用 *反向代理* 确保Primetime DRM Web应用程序的不同URL集可供外部和内部用户使用。 *反向代理* 比允许用户直接连接到运行Primetime DRM的应用程序服务器更安全，并且此配置对运行Primetime DRM的应用程序服务器执行所有HTTP请求。 用户只能访问反向代理，并且只能尝试反向代理支持的URL连接。

<!--<a id="fig_8083A8C794B646CD87985EC891B60663"></a>-->

![](assets/AdobeAccess_4_SecureDeployment.png)
