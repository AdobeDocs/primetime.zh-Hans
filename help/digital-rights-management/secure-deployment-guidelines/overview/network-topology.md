---
seo-title: 网络拓扑概述
title: 网络拓扑概述
uuid: b8b072dc-8dc0-46ba-bb01-1e9b58af2681
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# 概述{#network-topology-overview}

成功部署Adobe PrimetimeDRM后，您必须保持Primetime DRM制作服务器的安全性。

>[!NOTE]
>
>Primetime DRM之前被称为Adobe访问，在此之前称为Flash Access。

您可以使用&#x200B;*反向代理*&#x200B;确保外部和内部用户可以使用Primetime DRM Web应用程序的不同URL集。 *反向* 代理比允许用户直接连接到运行Primetime DRM的应用程序服务器更安全，此配置为运行Primetime DRM的应用程序服务器执行所有HTTP请求。用户只能访问反向代理，并且只能尝试反向代理支持的URL连接。

<!--<a id="fig_8083A8C794B646CD87985EC891B60663"></a>-->

![](assets/AdobeAccess_4_SecureDeployment.png)