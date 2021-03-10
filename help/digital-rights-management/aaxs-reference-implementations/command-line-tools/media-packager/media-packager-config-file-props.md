---
title: 配置文件属性
description: 配置文件属性
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---


# 配置文件属性{#configuration-file-properties}

运行Media Packager之前，请指定Media Packager属性的值。 配置文件指定以下属性。 对于包含* n*的属性名称，*n*&#x200B;表示从1开始的整数，并且该属性的每个实例都递增。

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_dx4_mpy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">属性 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">说明 </p> </th> 
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
   <td colname="2" class="- topic/entry ">指示是否加密FLV中的脚本数据。 <i class="+ topic/ph hi-d/i ">即</i> 使启用 <i class="+ topic/ph hi-d/i "></i> 了此选项，onMetaDat和onXMPscript数据标签也从未加密。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.video.level</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指示视频加密级别。 高值用于加密所有视频内容，而中值和低值用于加密包含H.264内容的F4V文件的视频内容的部分。 </p> <p class="- topic/p ">值= <span class="codeph"> |中 | low</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.secondsUnencrypted</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果值大于0，则不加密文件开头指定的秒数内容。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.ansymmet.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">用于加密密钥的许可证服务器证书文件。 <span class="codeph"> encrypt.keys.ansymet.certfile</span>属性指定仅包含证书的文件（PEM或DER格式可接受）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">encrypt.keys.policyFile.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">此属性用于重复创建要应用于内容的策略列表。 <span class="codeph"> </span> nis值为1或更大的整数。默认情况下，客户端将使用第一个实例。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverurl</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">许可证服务器URL。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.servercert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">许可证服务器的传输证书。 此属性指定仅包含证书的<span class="filepath"> .cer</span>文件（PEM或DER格式可接受）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">包含用于对内容进行签名的打包程序凭据的PKCS12文件。 <span class="codeph"> encrypt.sign.certfile</span>应引用包含证书和私钥的<span class="filepath"> .pfx</span>文件。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">用于保护由<span class="codeph"> encrypt.sign.certfile</span>指定的文件的口令。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.minServerVersion</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">设置为为要打包的内容颁发许可证所需的最低服务器版本。 指定x(Adobe访问x.0)，其中x =主发行号。 AdobeAccess 3.0之前的服务器不支持此设置。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.policyFile.n.domain.transportcert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果策略<span class="+ topic/ph pr-d/codeph codeph"> encrypt.keys.policyFile.n</span>需要向使用与<span class="+ topic/ph pr-d/codeph codeph"> encrypt.license.servercert</span>中指定的不同传输证书的服务器进行域注册，则需要提供域传输证书。 </p> <p class="- topic/p ">此属性指定仅包含证书的文件（PEM或DER格式可接受）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.licenseKey</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定许可证密钥。 如果未指定键，则将随机生成该键。 未启用密钥旋转时，这是用于加密内容的密钥。 </p> <p class="- topic/p ">启用键旋转时，此键用于保护旋转键。 键长必须为16个字节，并指定为十六进制值。 十六进制值之间的空格是可选的。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.enable</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定是否启用密钥旋转。 如果设置为false（默认），则禁用密钥旋转，并且主控CEK将用于加密内容中的所有样本。 </p> <p class="- topic/p ">如果设置为true，则将启用密钥旋转，并且可以使用不同的密钥加密内容的部分。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.rotation.key.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">用于在启用密钥旋转时加密内容的旋转密钥序列。 如果未指定任何键，则将随机生成键。 键的长度必须为16字节，并指定为十六进制值。 </p> <p class="- topic/p ">十六进制值之间的空格是可选的。 <i class="+ topic/ph hi-d/i ">必</i> 须从1开始单调增加。指定多个键时，按指示的顺序循环键。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.interval</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定使用旋转密钥加密内容范例的间隔（以秒为单位）。 </p> <p class="- topic/p ">在内容中的此时间量经过加密后，将使用下一个旋转密钥。 如果启用了密钥旋转并且未指定间隔，则每15分钟旋转一次密钥。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverless</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果为true，则不存在可从中获取许可证的许可证服务器。 许可证必须嵌入或带外获得。 如果未指定，则默认值为false。 仅在Adobe Access Professional中受支持。 </p> </td> 
  </tr> 
 </tbody> 
</table>

