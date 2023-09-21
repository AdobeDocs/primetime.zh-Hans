---
title: Adobe访问使用的网络协议
description: Adobe访问使用的网络协议
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# Adobe访问使用的网络协议 {#network-protocols-used-by-adobe-access}

在配置安全网络体系结构时，下表中的网络协议是Adobe访问与企业网络中的其他系统之间交互所必需的。

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Flash Player 、 Adobe AIR®和Adobe Primetime客户端通过HTTP与Adobe访问进行通信。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTPS（可选） </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Flash Player、Adobe AIR和Adobe Primetime客户端可以使用HTTPS与Adobe访问进行通信，但是，除非您需要对FMRMS 1.x客户端的支持，否则不需要HTTPS (SSL)。 请参阅表中的注释 <a href="network-topology-firewall-rules.md" format="dita" scope="local"> 传入URL</a> 和 <a href="network-topology-nw-protocols.md"> 配置SSL</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>
