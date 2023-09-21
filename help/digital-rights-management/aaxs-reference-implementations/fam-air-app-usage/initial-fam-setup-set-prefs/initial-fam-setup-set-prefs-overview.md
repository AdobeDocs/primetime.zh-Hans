---
title: 设置首选项概述
description: 设置首选项概述
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---

# 设置首选项概述 {#setting-preferences-overview}

除Packager服务器URL外，下面指定的所有首选项都存储在 [!DNL flashaccess-refimpl-packager.properties] 文件中的文件。 所有设置可以直接在属性文件中修改，也可以通过AIR应用程序进行修改。 当密码存储在服务器上的属性文件中时，就会对其进行加密。 在UI中键入未加密的密码，该密码将在存储到文件之前进行加密。

>[!NOTE]
>
>所有目录和路径都引用Packager服务器上的目录，而不是运行AIR应用程序的客户端上的目录。

此处所做的任何更改在保存首选项后立即生效。 除非由于配置问题而终止了打包程序线程，否则无需重新启动服务器。

首选项描述使用以下术语：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_tj5_hcz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> 首选项 </th> 
   <th colname="2" class="- topic/entry entry"> 描述 </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> Packager服务器URL </td> 
   <td colname="2" class="- topic/entry "> 正在运行的服务器的位置 <span class="filepath"> flashaccess-packager.war </span>；例如， <span class="filepath"> https://localhost:8080 </span> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 资源目录 </td> 
   <td colname="2" class="- topic/entry "> 包含打包服务器所需的策略、证书、凭据和任何其他资源的目录 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 许可证服务器URL </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">客户端应从中请求许可证的服务器的URL；例如， <span class="filepath"> https://mylicenseserver.com:8080 </span> </p> </td> 
  </tr> 
 </tbody> 
</table>
