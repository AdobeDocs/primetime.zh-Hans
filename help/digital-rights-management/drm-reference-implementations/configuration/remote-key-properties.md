---
title: 远程密钥投放属性(iOS)
description: 远程密钥投放属性(iOS)
copied-description: true
exl-id: 0fe3ed9b-a8ee-43b4-ab3c-8ea2e696503b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---

# 远程密钥投放属性(iOS){#remote-key-delivery-properties-ios}

要支持生成用于在Adobe Primetime DRM中向iOS客户端交付远程密钥的许可证，您必须在中指定密钥服务器证书 `flashaccess-refimpl.properties` 文件。

Primetime DRM中添加了以下属性：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_xz2_lwy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">属性 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">描述 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> HandlerConfiguration.KeyServerCertificate</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Adobe颁发的密钥服务器的许可证服务器证书。 </p> <p>当元数据指示需要密钥服务器时，此证书会为iOS设备生成许可证。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> RefImpl.HSM.HandlerConfiguration.\ KeyServerCertificate.Alias</span> </td> 
   <td colname="2" class="- topic/entry "> <p>Key ServerAdobe颁发的License Server证书的别名，存储在HSM上。 </p> <p>启用HSM后，您可以应用此属性而不是 <span class="codeph"> HandlerConfiguration.KeyServerCertificate</span> 属性。 </p> </td> 
  </tr> 
 </tbody> 
</table>
