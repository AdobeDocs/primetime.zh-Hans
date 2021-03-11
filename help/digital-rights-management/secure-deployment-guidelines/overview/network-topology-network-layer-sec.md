---
description: 网络安全漏洞是任何面向Internet或面向Intranet的应用程序服务器面临的首要威胁之一，您必须针对这些漏洞加强网络上的主机。
title: 网络层安全
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---


# 网络层安全性{#network-layer-security}

网络安全漏洞是任何面向Internet或面向Intranet的应用程序服务器面临的首要威胁之一，您必须针对这些漏洞加强网络上的主机。

以下是一些减少网络安全漏洞的常用技术：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_djf_lhz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">技术 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">说明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">非军事区(DMZ) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">分段必须至少存在于两个级别，当Primetime DRM位于内部防火墙后时，应用程序服务器用于运行Adobe Primetime DRM。 您必须将外部网络与包含Web服务器的DMZ分离，并且Web服务器必须与内部网络分离。 您可以使用防火墙来实现这些隔离层。 </p> <p>您可以对流经每个网络层的流量进行分类和控制，以确保仅允许所需数据的绝对最小值。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">专用IP地址 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">在Primetime DRM应用程序服务器上将网络地址转换(NAT)与RFC 1918专用IP地址结合使用。 您可以分配专用IP地址(10.0.0.0/8、172.16.0.0/12和192.168.0.0/16)，使攻击者更难通过Internet将通信路由到NAT内部主机和从NAT内部主机。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">防火墙 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">以下是选择防火墙解决方案时要考虑的一些标准： </p> <p class="- topic/p "> 
     <ul class="- topic/ul " id="ul_wjf_lhz_n4"> 
      <li class="- topic/li " id="li_A620D0B635384590BA7804F9720D04D0">实施支持代理服务器和/或状态检查的防火墙，而不是简单的数据包过滤解决方案。 </li> 
      <li class="- topic/li " id="li_3E4F814A30C047539185C23F4F57C282">使用支持安全模式的防火墙，在这种模式下，您可以拒绝除明确允许的服务之外的所有服务。 </li> 
      <li class="- topic/li " id="li_96160B3F14C4425397F017AF93FABE32">实施双宿或多宿的防火墙解决方案。 此体系结构提供最高级别的安全性，并防止未经授权的用户绕过防火墙安全。 </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

