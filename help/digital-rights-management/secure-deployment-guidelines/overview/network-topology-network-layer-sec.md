---
description: 网络安全漏洞是任何面向Internet或内联网的应用程序服务器的首要威胁之一，您必须加强网络上的主机来抵御这些漏洞。
title: 网络层安全性
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# 网络层安全性{#network-layer-security}

网络安全漏洞是任何面向Internet或内联网的应用程序服务器的首要威胁之一，您必须加强网络上的主机来抵御这些漏洞。

以下是减少网络安全漏洞的一些常用技术：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_djf_lhz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">技术 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">描述 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">非军事区(DMZ) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">当Primetime DRM位于内部防火墙后面时，必须使用用于运行Adobe Primetime DRM的应用程序服务器至少存在两个级别的分段。 您必须将外部网络与包括Web服务器的DMZ分开，并且Web服务器必须与内部网络分开。 您可以使用防火墙实现这些分隔层。 </p> <p>您可以对经过每个网络层的流量进行分类并加以控制，以确保仅允许使用绝对最小所需数据。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">私有IP地址 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">在Primetime DRM应用程序服务器上将网络地址转换(NAT)与RFC 1918专用IP地址一起使用。 您可以分配私有IP地址(10.0.0.0/8、172.16.0.0/12和192.168.0.0/16)，使攻击者通过Internet在NAT内部主机之间路由通信更加困难。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">防火墙 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">选择防火墙解决方案时要考虑以下一些标准： </p> <p class="- topic/p "> 
     <ul class="- topic/ul " id="ul_wjf_lhz_n4"> 
      <li class="- topic/li " id="li_A620D0B635384590BA7804F9720D04D0">实施支持代理服务器和/或状态检查的防火墙，而不是简单的数据包过滤解决方案。 </li> 
      <li class="- topic/li " id="li_3E4F814A30C047539185C23F4F57C282">使用支持安全模式的防火墙，在该防火墙中，您可以拒绝所有服务，但明确允许的服务除外。 </li> 
      <li class="- topic/li " id="li_96160B3F14C4425397F017AF93FABE32">实施双宿主或多宿主的防火墙解决方案。 此架构可提供最高级别的安全性，并防止未经授权的用户绕过防火墙的安全性。 </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
