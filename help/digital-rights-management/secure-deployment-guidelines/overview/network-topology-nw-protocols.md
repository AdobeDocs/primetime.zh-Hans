---
description: 配置安全网络架构时，在Adobe PrimetimeDRM与企业网络中的其他系统之间进行交互时，需要使用网络协议。
seo-description: 配置安全网络架构时，在Adobe PrimetimeDRM与企业网络中的其他系统之间进行交互时，需要使用网络协议。
seo-title: Adobe PrimetimeDRM网络协议
title: Adobe PrimetimeDRM网络协议
uuid: 8954e33c-83ac-4b40-9e45-005d4954b44e
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---


# Adobe PrimetimeDRM网络协议{#adobe-primetime-drm-network-protocols}

配置安全网络架构时，在Adobe PrimetimeDRM与企业网络中的其他系统之间进行交互时，需要使用网络协议。

配置安全网络架构时，此交互需要以下网络协议：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_itc_33z_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">协议 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">使用 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTP </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Flash Player、Adobe AIR®和Adobe Primetime客户端通过HTTP与Primetime DRM进行通信。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTPS（可选） </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Flash Player、Adobe AIR和Adobe Primetime客户可以使用HTTPS与Primetime DRM进行通信；除非您支持FMRMS 1.x客户端，否则不需要HTTPS(SSL)。 有关详细信息，请参阅<a href="../../secure-deployment-guidelines/overview/network-topology-firewall-rules.md" format="dita" scope="local">传入URL </a>和配置SSL。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 应用程序服务器{#ports-for-application-servers}的端口

您可以配置Adobe PrimetimeDRM许可证服务器以使用任何网络端口。

这些端口必须在内部防火墙上启用或禁用，具体取决于您希望允许连接到运行Primetime DRM的应用程序服务器的客户端的网络功能。

## 配置SSL {#configuring-ssl}

仅当需要支持Flash媒体Rights Management服务器1.x客户端时，才需要安全套接字层(SSL)。

Adobe PrimetimeDRM密钥服务器需要使用客户端身份验证的SSL。 有关详细信息，请参阅[使用Adobe PrimetimeDRM密钥服务器](../../using-the-drm-key-server/requirements.md)。