---
title: 远程密钥投放属性(iOS)
description: 远程密钥投放属性(iOS)
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---


# 远程密钥投放属性(iOS){#remote-key-delivery-properties-ios}

要支持为Adobe Primetime DRM中的iOS客户端生成远程密钥投放的许可证，必须在`flashaccess-refimpl.properties`文件中指定密钥服务器证书。

Primetime DRM中已添加以下属性：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_xz2_lwy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">属性 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">说明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> HandlerConfiguration.KeyServerCertificate</span> </td> 
   <td colname="2" class="- topic/entry "> <p>由Adobe颁发的密钥服务器的许可证服务器证书。 </p> <p>当元数据指示需要密钥服务器时，此证书将为iOS设备生成许可证。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> RefImpl.HSM.HandlerConfiguration。\ KeyServerCertificate.Alias</span> </td> 
   <td colname="2" class="- topic/entry "> <p>存储在HSM上的密钥服务器Adobe颁发的许可证服务器证书的别名。 </p> <p>启用HSM时，可以应用此属性，而不是<span class="codeph"> HandlerConfiguration.KeyServerCertificate</span>属性。 </p> </td> 
  </tr> 
 </tbody> 
</table>

