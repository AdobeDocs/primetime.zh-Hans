---
title: 许可证服务器属性文件
description: 许可证服务器属性文件
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# 许可证服务器属性文件 {#license-server-properties-file}

使用 [!DNL flashaccess-refimpl.properties] 文件，用于配置参考实施的许可证服务器组件。 至少要确保配置与传输凭据和许可证服务器凭据相关的属性。 必须指定凭据文件的位置，并且位置必须相对于指定的目录 `config.resourcesDirectory` 属性。 此文件还包含与打包内容相关的几个属性：这些属性仅用于FlashMediaRights Management服务器1.x元数据转换。 如果修改此属性文件中的任何值，则需要重新启动许可证服务器以使更改生效。

要支持在Adobe访问中生成向iOS客户端交付远程密钥的许可证，必须在中指定密钥服务器证书 [!DNL flashaccess-refimpl.properties].

Adobe访问中添加了以下属性：

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
   <td colname="2" class="- topic/entry "> Key Server的License Server证书，由Adobe颁发。 当元数据指示需要密钥服务器时，此证书用于为iOS设备生成许可证。 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> RefImpl.HSM.HandlerConfiguration.\ KeyServerCertificate.Alias</span> </td> 
   <td colname="2" class="- topic/entry ">Key ServerAdobe颁发的License Server证书的别名，存储在HSM上。 启用HSM后，请使用此属性而不是 <span class="codeph"> HandlerConfiguration.KeyServerCertificate</span>. </td> 
  </tr> 
 </tbody> 
</table>
