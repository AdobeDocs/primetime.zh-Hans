---
seo-title: 许可证服务器属性文件
title: 许可证服务器属性文件
uuid: bede307a-2060-451f-baf5-d058702c0a7e
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# 许可证服务器属性文件{#license-server-properties-file}

使用[!DNL flashaccess-refimpl.properties]文件配置引用实现的License Server组件。 至少要配置与传输凭据和许可证服务器凭据相关的属性。 必须相对于`config.resourcesDirectory`属性指定的目录指定凭据文件的位置。 此文件还包含与打包内容相关的若干属性：这些属性仅用于Flash媒体Rights Management服务器1.x元数据转换。 如果修改此属性文件中的任何值，您需要重新启动许可证服务器才能使更改生效。

要支持在Adobe访问中为iOS客户端生成远程密钥投放的许可证，必须在[!DNL flashaccess-refimpl.properties]中指定密钥服务器证书。

在Adobe访问中添加了以下属性：

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
   <td colname="2" class="- topic/entry "> 密钥服务器的许可证服务器证书，由Adobe颁发。 当元数据指示需要密钥服务器时，此证书用于为iOS设备生成许可证。 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> RefImpl.HSM.HandlerConfiguration。\ KeyServerCertificate.Alias</span> </td> 
   <td colname="2" class="- topic/entry ">存储在HSM上的密钥服务器Adobe颁发的许可证服务器证书的别名。 启用HSM时，请使用此属性，而不是<span class="codeph"> HandlerConfiguration.KeyServerCertificate</span>。 </td> 
  </tr> 
 </tbody> 
</table>

