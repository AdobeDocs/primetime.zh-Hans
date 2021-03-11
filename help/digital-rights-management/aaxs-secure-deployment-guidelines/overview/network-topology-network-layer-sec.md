---
title: 网络层安全
description: 网络层安全
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---


# 网络层安全性{#network-layer-security}

网络安全漏洞是任何面向Internet或面向Intranet的应用程序服务器面临的首要威胁之一。 本节介绍针对这些漏洞强化网络上的主机的过程。 它解决了网络分段、传输控制协议/因特网协议(TCP/IP)栈加固以及使用防火墙保护主机的问题。

下表描述了减少网络安全漏洞的常用技术。

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-djf-lhz-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">技术 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">说明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">非军事区(DMZ) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">分段必须至少存在于两个级别中，应用程序服务器用于运行位于内部防火墙后的Adobe访问。 将外部网络与包含Web服务器的DMZ分离，而Web服务器又必须与内部网络分离。 使用防火墙实现隔离层。 对通过每个网络层的流量进行分类和控制，以确保仅允许绝对最少的所需数据。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">专用IP地址 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">将网络地址转换(NAT)与Adobe Access应用程序服务器上的RFC 1918专用IP地址结合使用。 分配专用IP地址(10.0.0.0/8、172.16.0.0/12和192.168.0.0/16)，使攻击者更难通过Internet将通信路由到NAT内部主机和从内部主机。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">防火墙 </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">使用以下条件选择防火墙解决方案： </p> <p class="- topic/p "> 
     <ul class="- topic/ul " id="ul-wjf-lhz-n4"> 
      <li class="- topic/li " id="li-8031632160F44037B092988183139202"> <p class="- topic/p ">实施防火墙，它们支持代理服务器和/或状态检查，而不是简单的数据包过滤解决方案。 </p> </li> 
      <li class="- topic/li " id="li-B65CBB92113E4503B79EB194C34FCA50"> <p class="- topic/p ">使用支持安全模式的防火墙，在这种模式下，您可以拒绝除明确允许的服务外的所有服务。 </p> </li> 
      <li class="- topic/li " id="li-5CE4C7B65D84410DB4BE966FD8922993"> <p class="- topic/p ">实施双宿或多宿的防火墙解决方案。 此体系架构提供最高级别的安全性，并有助于防止未经授权的用户绕过防火墙安全。 </p> </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

