---
seo-title: 许可证服务器属性文件
title: 许可证服务器属性文件
uuid: bede307a-2060-451f-baf5-d058702c0a7e
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 许可证服务器属性文件 {#license-server-properties-file}

使用该文 [!DNL flashaccess-refimpl.properties] 件配置参考实施的许可证服务器组件。 至少，请务必配置与传输凭证和许可证服务器凭证相关的属性。 必须指定凭证文件的位置相对于属性指定的目录的相 `config.resourcesDirectory` 对位置。 此文件还包含与打包内容相关的几个属性：这些属性仅用于Flash Media Rights Management Server 1.x元数据转换。 如果修改了此属性文件中的任意值，则需要重新启动许可证服务器，以使更改生效。

要支持为在Adobe Access中向iOS客户端交付远程密钥生成许可证，必须在中指定密钥服务器证书 [!DNL flashaccess-refimpl.properties]。

Adobe Access中已添加以下属性：

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
   <td colname="2" class="- topic/entry "> Adobe颁发的Key Server许可证服务器证书。 当元数据指示需要密钥服务器时，此证书用于为iOS设备生成许可证。 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> RefImpl.HSM.HandlerConfiguration。\ KeyServerCertificate.Alias</span> </td> 
   <td colname="2" class="- topic/entry ">密钥服务器在HSM上存储的Adobe颁发的许可证服务器证书的别名。 启用HSM后，请使用此属性，而不 <span class="codeph"> 是HandlerConfiguration.KeyServerCertificate</span>。 </td> 
  </tr> 
 </tbody> 
</table>

