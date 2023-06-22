---
title: 配置文件属性
description: 配置文件属性
copied-description: true
exl-id: ce4193fa-d217-4134-b08e-715c2cc57c84
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# 配置文件属性 {#configuration-file-properties}

在运行许可证生成器之前，请为许可证生成器属性指定值。 配置文件指定以下属性。 对于包含的属性名称 *n*， *n* 表示一个整数，从1开始，对于属性的每个实例都增大。

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_qk1_rry_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> 属性 </th> 
   <th colname="2" class="- topic/entry entry"> 描述 </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.minClientVersion</span> </td> 
   <td colname="2" class="- topic/entry "> 设置支持的最低客户端版本。 如果未设置，则默认支持所有版本。 设置此值以控制旧版客户端如何响应它们不支持的许可证要求。 指定x(用于Adobe访问x.0)，其中x是主要发行版本号。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.keyServerCert</span> </td> 
   <td colname="2" class="- topic/entry "> 密钥服务器证书(密钥服务器使用的Adobe颁发的许可证服务器证书)。 仅当元数据/策略指示需要密钥服务器才能将密钥交付到iOS设备时，才使用此证书。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> 包含用于签署许可证的许可证服务器凭据的PKCS12文件。 此属性应引用包含证书和私钥的.pfx文件。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry ">用于保护指定文件的密码 <span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certfile。</span> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.domainca.n</span> </td> 
   <td colname="2" class="- topic/entry "> 如果生成绑定域的许可证，则必须指定一个或多个域CA证书，以指示此许可证颁发者信任的域颁发机构。 如果许可证收件人不是由指定的域CA之一颁发的域证书，则无法生成许可证。 此属性指定仅包含证书的.cer文件（可以接受PEM或DER格式）。 n必须从1开始单调递增。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.keys.asymmetric.licenseServerCredential.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">可选PKCS12文件，其中包含用于解密元数据和策略中的CEK的其他许可证服务器凭据。 如果内容先前是使用许可证服务器证书而不是指定的证书打包的，则可以配置其他凭据 <span class="codeph"> licensegen.sign.certfile</span>. 此属性应该指的是 <span class="filepath"> .pfx</span> 包含证书和私钥的文件。 n必须从1开始单调递增。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.keys.asymmetric.licenseServerCredential.n.password</span> </td> 
   <td colname="2" class="- topic/entry ">用于保护文件的密码，指定者： <p><span class="+ topic/ph pr-d/codeph codeph"> licensegen.keys.asymmetric.licenseServerCredential.n</span> </p> </td> 
  </tr> 
 </tbody> 
</table>
