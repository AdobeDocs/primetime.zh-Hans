---
title: Adobe访问使用的网络协议
description: Adobe访问使用的网络协议
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---


# Adobe访问{#network-protocols-used-by-adobe-access}使用的网络协议

配置安全网络架构时，需要下表中的网络协议才能在Adobe Access与企业网络中的其他系统之间进行交互。

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-itc-33z-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">协议 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">使用 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTP </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Flash Player、Adobe AIR®和Adobe Primetime客户端通过HTTP与Adobe Access进行通信。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTPS（可选） </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Flash Player、Adobe AIR和Adobe Primetime客户端可以使用HTTPS与Adobe Access进行通信，但是，除非您需要FMRMS 1.x客户端支持，否则不需要HTTPS(SSL)。 请参见表<a href="network-topology-firewall-rules.md" format="dita" scope="local">传入URL</a>和<a href="network-topology-nw-protocols.md">配置SSL</a>中的说明。 </p> </td> 
  </tr> 
 </tbody> 
</table>