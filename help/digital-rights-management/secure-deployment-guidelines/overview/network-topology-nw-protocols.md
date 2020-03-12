---
description: 配置安全网络架构时，Adobe Primetime DRM与企业网络中的其他系统之间的交互需要网络协议。
seo-description: 配置安全网络架构时，Adobe Primetime DRM与企业网络中的其他系统之间的交互需要网络协议。
seo-title: Adobe Primetime DRM网络协议
title: Adobe Primetime DRM网络协议
uuid: 8954e33c-83ac-4b40-9e45-005d4954b44e
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Adobe Primetime DRM网络协议 {#adobe-primetime-drm-network-protocols}

配置安全网络架构时，Adobe Primetime DRM与企业网络中的其他系统之间的交互需要网络协议。

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Flash Player、Adobe AIR®和Adobe Primetime客户端通过HTTP与Primetime DRM通信。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTPS（可选） </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Flash Player、Adobe AIR和Adobe Primetime客户端可以使用HTTPS与Primetime DRM通信；除非您支持FMRMS 1.x客户端，否则不需要HTTPS(SSL)。 有关详细信息，请参 <a href="../../secure-deployment-guidelines/overview/network-topology-firewall-rules.md" format="dita" scope="local"> 阅传入URL </a> 和配置SSL。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 应用程序服务器的端口 {#ports-for-application-servers}

您可以配置Adobe Primetime DRM许可证服务器以使用任何网络端口。

这些端口必须在内部防火墙上启用或禁用，具体取决于您希望允许连接到运行Primetime DRM的应用程序服务器的客户端的网络功能。

## 配置SSL {#configuring-ssl}

只有在需要Flash Media Rights Management Server 1.x客户端支持时，才需要安全套接字层(SSL)。

Adobe Primetime DRM Key Server需要具有客户端身份验证的SSL。 有关详细信息，请 [参阅使用Adobe Primetime DRM Key Server](../../using-the-drm-key-server/requirements.md)。