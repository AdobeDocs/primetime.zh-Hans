---
title: 网络层安全性
description: 网络层安全性
copied-description: true
exl-id: 70c9917d-32bc-43f6-add3-62883f98ac5e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# 网络层安全性{#network-layer-security}

网络安全漏洞是对任何面向Internet或面向Intranet的应用程序服务器的首要威胁之一。 本节将介绍增强网络上的主机抵御这些漏洞的过程。 它涉及网络分段、传输控制协议/Internet协议(TCP/IP)栈栈强化，以及使用防火墙进行主机保护。

此表介绍了减少网络安全漏洞的常用技术。

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-djf-lhz-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">技术 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">描述 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">非军事区(DMZ) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">分段必须至少存在于两个级别，并且应用程序服务器用于运行Adobe访问，并且放置在内部防火墙内。 将外部网络与包含Web服务器的DMZ分开，而后者则必须与内部网络分开。 使用防火墙实现分隔层。 对经过每个网络层的流量进行分类并加以控制，以确保仅允许所需数据的绝对最小值。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">专用IP地址 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">在Adobe访问应用程序服务器上将网络地址转换(NAT)与RFC 1918专用IP地址结合使用。 分配私有IP地址(10.0.0.0/8、172.16.0.0/12和192.168.0.0/16)，使攻击者更难以通过Internet来路由往来于NAT内部主机的流量。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">防火墙 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">使用以下标准选择防火墙解决方案： </p> <p class="- topic/p "> 
     <ul class="- topic/ul " id="ul-wjf-lhz-n4"> 
      <li class="- topic/li " id="li-8031632160F44037B092988183139202"> <p class="- topic/p ">实施支持代理服务器和/或状态检查的防火墙，而不是简单的包过滤解决方案。 </p> </li> 
      <li class="- topic/li " id="li-B65CBB92113E4503B79EB194C34FCA50"> <p class="- topic/p ">使用支持安全模式的防火墙，在该模式下，您可以拒绝所有服务，但明确允许的服务除外。 </p> </li> 
      <li class="- topic/li " id="li-5CE4C7B65D84410DB4BE966FD8922993"> <p class="- topic/p ">实施双宿主或多宿主的防火墙解决方案。 此架构提供最高级别的安全性，并有助于防止未经授权的用户绕过防火墙的安全性。 </p> </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
