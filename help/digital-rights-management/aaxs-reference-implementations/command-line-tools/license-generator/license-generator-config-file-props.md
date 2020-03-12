---
seo-title: 配置文件属性
title: 配置文件属性
uuid: 13e158a6-c447-4e5e-884d-03fb4835c120
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 配置文件属性 {#configuration-file-properties}

运行许可证生成器之前，请指定许可证生成器属性的值。 配置文件指定以下属性。 对于包含n的属 *性名称*, ** n表示从1开始的整数，并且对于属性的每个实例都递增。

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_qk1_rry_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> 属性 </th> 
   <th colname="2" class="- topic/entry entry"> 说明 </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.minClientVersion</span> </td> 
   <td colname="2" class="- topic/entry "> 设置支持的最低客户端版本。 如果未设置，默认情况下支持所有版本。 设置此值，以控制老客户如何响应他们不支持的许可证要求。 指定x（对于Adobe Access x.0），其中x是主要版本号。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.keyServerCert</span> </td> 
   <td colname="2" class="- topic/entry "> 密钥服务器证书（由密钥服务器使用的Adobe颁发的许可证服务器证书）。 仅当元数据／策略指示向iOS设备传送密钥需要密钥服务器时，才使用此证书。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> 包含用于签署许可证的许可证服务器凭据的PKCS12文件。 此属性应引用包含证书和私钥的。pfx文件。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry ">用于保护由licensegen.sign.certfile指定 <span class="+ topic/ph pr-d/codeph codeph"> 的文件的口令。</span> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.domainca.n</span> </td> 
   <td colname="2" class="- topic/entry "> 如果生成域绑定许可证，则必须指定一个或多个域CA证书以指示此许可证颁发者信任的域授权。 如果许可证接收者是域证书，而该证书不是由指定的域CA之一颁发的，则无法生成许可证。 此属性指定仅包含证书的。cer文件（PEM或DER格式可接受）。 n必须是单调递增的，从1开始。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.keys.ansymmetric.licenseServerCredential.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">可选的PKCS12文件，其中包含用于在元数据和策略中解密CEK的其他许可证服务器凭据。 如果内容之前与许可证服务器证书打包在一起，而不是由licensegen.sign.certfile指定的证书，则可以配置 <span class="codeph"> 其他凭据</span>。 此属性应引用包含证 <span class="filepath"> 书和私钥的</span> .pfx文件。 n必须是单调递增的，从1开始。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.keys.ansymetric.licenseServerCredential.n.password</span> </td> 
   <td colname="2" class="- topic/entry ">用于保护由以下人员指定的文件的口令： <p><span class="+ topic/ph pr-d/codeph codeph"> licensegen.keys.ansymmetric.licenseServerCredential.n</span> </p> </td> 
  </tr> 
 </tbody> 
</table>

