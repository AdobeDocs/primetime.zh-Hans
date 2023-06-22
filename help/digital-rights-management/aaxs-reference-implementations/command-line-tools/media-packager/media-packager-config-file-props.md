---
title: 配置文件属性
description: 配置文件属性
copied-description: true
exl-id: eec6a53d-d831-4ec4-a90c-8b3e7997f330
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---

# 配置文件属性 {#configuration-file-properties}

运行Media Packager之前，请指定Media Packager属性的值。 配置文件指定以下属性。 对于包含* n*的属性名称， *n* 表示一个整数，从1开始，对于属性的每个实例都增大。

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_dx4_mpy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">属性 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">描述 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.video</span> </td> 
   <td colname="2" class="- topic/entry "> 指示是否加密视频内容。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.audio</span> </td> 
   <td colname="2" class="- topic/entry "> 指示是否加密音频。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.script</span> </td> 
   <td colname="2" class="- topic/entry ">指示是否加密FLV中的脚本数据。 <i class="+ topic/ph hi-d/i ">onMetaData</i> 和 <i class="+ topic/ph hi-d/i ">onXMP</i> 即使启用了此选项，脚本数据标记也不会加密。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.video.level</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指示视频加密级别。 高值用于加密所有视频内容，而中值和低值用于加密包含H.264内容的F4V文件的部分视频内容。 </p> <p class="- topic/p ">值= <span class="codeph"> 高 |中 |低</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.seconds未加密</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果该值大于0，则不会加密文件开头指定的内容秒数。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.asymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">用于加密密钥的许可证服务器证书文件。 此 <span class="codeph"> encrypt.keys.asymmetric.certfile</span> 属性指定仅包含证书的文件（可接受PEM或DER格式）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">encrypt.keys.policyFile.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">此属性被重复用于创建要应用于内容的策略列表。 <span class="codeph"> n</span> 是一个整数，其值为1或更大。 默认情况下，客户端将使用第一个实例。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverurl</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">许可证服务器URL。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.servercert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">许可证服务器的传输证书。 此属性指定 <span class="filepath"> .cer</span> 仅包含证书的文件（可接受PEM或DER格式）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">包含用于签名内容的打包程序凭据的PKCS12文件。 此 <span class="codeph"> encrypt.sign.certfile</span> 应该指的是 <span class="filepath"> .pfx</span> 包含证书和私钥的文件。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">用于保护指定文件的密码 <span class="codeph"> encrypt.sign.certfile</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.minServerVersion</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">设置为要打包的内容颁发许可证所需的最低服务器版本。 指定x(Adobe访问x.0)，其中x =主要版本号。 Adobe访问3.0之前的服务器不支持此设置。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.policyFile.n.domain.transportcert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果策略 <span class="+ topic/ph pr-d/codeph codeph"> encrypt.keys.policyFile.n</span> 要求使用不同于中指定的传输证书的服务器进行域注册 <span class="+ topic/ph pr-d/codeph codeph"> encrypt.license.servercert</span>，需要提供域传输证书。 </p> <p class="- topic/p ">此属性指定仅包含证书的文件（可以接受PEM或DER格式）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.licenseKey</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定许可证密钥。 如果未指定密钥，则将随机生成密钥。 如果未启用密钥轮替，则这是用于加密内容的密钥。 </p> <p class="- topic/p ">启用密钥轮换后，将使用此密钥保护轮换密钥。 密钥长度必须为16个字节，并指定为十六进制值。 十六进制值之间的空格是可选的。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.enable</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定是否启用密钥轮替。 如果设置为false（默认），将禁用密钥轮换，并将使用主控CEK加密内容中的所有示例。 </p> <p class="- topic/p ">如果设置为true，将启用密钥轮换，并且可以使用不同的密钥来加密内容的各个部分。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.rotation.key.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">启用密钥轮替后，用于对内容进行加密的轮替密钥序列。 如果未指定密钥，则将随机生成密钥。 密钥长度必须为16个字节，并指定为十六进制值。 </p> <p class="- topic/p ">十六进制值之间的空格是可选的。 <i class="+ topic/ph hi-d/i ">n</i> 必须单调递增，从1开始递增。 指定多个键时，键将按指示的顺序循环使用。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.interval</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定使用轮换密钥加密内容示例的时间间隔（以秒为单位）。 </p> <p class="- topic/p ">在加密内容中的这段时间后，将使用下一个轮换密钥。 如果启用了密钥轮换并且未指定时间间隔，则将每15分钟轮换一次密钥。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverless</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果为true，则没有许可证服务器可从其中获取许可证。 必须嵌入许可证或在带外获取许可证。 如果未指定，则默认值为false。 仅在Adobe Access Professional中受支持。 </p> </td> 
  </tr> 
 </tbody> 
</table>
