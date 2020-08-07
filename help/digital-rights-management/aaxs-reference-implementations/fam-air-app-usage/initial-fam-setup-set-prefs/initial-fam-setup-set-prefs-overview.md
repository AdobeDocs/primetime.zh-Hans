---
seo-title: 设置首选项概述
title: 设置首选项概述
uuid: d1c067b1-6c2b-460e-8d00-5a5bfee0789c
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# 设置首选项概述 {#setting-preferences-overview}

除Packager Server URL外，下面指定的所有首选项都存储在服务器上的 [!DNL flashaccess-refimpl-packager.properties] 文件中。 所有设置都可以直接在属性文件中或通过AIR应用程序进行修改。 口令存储在服务器的属性文件中时会加密。 在UI中键入未加密的密码，在将其存储到文件中之前，将对其进行加密。

>[!NOTE]
>
>所有目录和路径引用打包程序服务器上的目录，而不是运行AIR应用程序的客户端上的目录。

保存首选项后，此处所做的任何更改将立即生效。 无需重新启动服务器，除非Packager线程因配置问题而终止。

首选项描述使用以下术语：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_tj5_hcz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> 首选项 </th> 
   <th colname="2" class="- topic/entry entry"> 说明 </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> Packager服务器URL </td> 
   <td colname="2" class="- topic/entry "> 运行flashaccess- <span class="filepath"> packager.war的服务器的位置 </span>;例如 <span class="filepath"> https://localhost:8080 </span> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 资源目录 </td> 
   <td colname="2" class="- topic/entry "> 包含策略、证书、凭据以及打包服务器所需的任何其他资源的目录 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 许可证服务器URL </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">客户端应从中请求许可证的服务器URL;例如 <span class="filepath"> https://mylicenseserver.com:8080 </span> </p> </td> 
  </tr> 
 </tbody> 
</table>

