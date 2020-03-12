---
seo-title: Adobe Access使用的网络协议
title: Adobe Access使用的网络协议
uuid: 4f2ee3f5-6758-4fbe-b5cd-cead1e5ccde8
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Adobe Access使用的网络协议 {#network-protocols-used-by-adobe-access}

配置安全网络架构时，Adobe Access与企业网络中其他系统之间的交互需要下表中的网络协议。

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Flash Player、Adobe AIR®和Adobe Primetime客户端通过HTTP与Adobe Access通信。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTPS（可选） </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Flash Player、Adobe AIR和Adobe Primetime客户端可以使用HTTPS与Adobe Access进行通信，但是，除非您需要FMRMS 1.x客户端支持，否则不需要HTTPS(SSL)。 请参阅表“传入的URL <a href="network-topology-firewall-rules.md" format="dita" scope="local"> ”和</a> “配置 <a href="network-topology-nw-protocols.md"> SSL”中的说明</a>。 </p> </td> 
  </tr> 
 </tbody> 
</table>