---
title: 网络拓扑概述
description: 网络拓扑概述
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# 概述{#network-topology-overview}

成功部署Adobe Primetime DRM后，您必须保持Primetime DRM制作服务器的安全性。

>[!NOTE]
>
>Primetime DRM以前称为Adobe访问，在此之前称为Flash Access。

您可以使用&#x200B;*反向代理*&#x200B;来确保外部和内部用户可以使用Primetime DRM Web应用程序的不同URL集。 *反向* 代理比允许用户直接连接到运行Primetime DRM的应用程序服务器更安全，此配置为运行Primetime DRM的应用程序服务器执行所有HTTP请求。用户只能访问反向代理，并只能尝试反向代理支持的URL连接。

<!--<a id="fig_8083A8C794B646CD87985EC891B60663"></a>-->

![](assets/AdobeAccess_4_SecureDeployment.png)