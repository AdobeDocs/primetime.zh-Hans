---
title: 概述
description: 概述
copied-description: true
exl-id: 866b3147-c28b-41b0-8653-06ba867354c5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 0%

---

# DRM Media Packager {#media-packager}

使用Media Packager ( [!DNL AdobePackager.jar])，以指定要应用于内容的DRM策略，并指定要加密的内容部分。 例如，您可以指定打包程序应加密视频数据，但不加密音频数据。

运行之前 [!DNL AdobePackager.jar]，您必须在配置文件的Media Packager属性部分设置属性。

>[!NOTE]
>
>还可以从命令行指定所有Media Packager属性。

## Media Packager命令行用法 {#media-packager-command-line-usage}

**打包一个文件：**

```
java -jar AdobePackager.jar  
<i class="+ topic ph hi-d="" i "="">
  source  
 <i class="+ topic ph hi-d="" i "="">
   dest [ 
  <i class="+ topic ph hi-d="" i "="">
    options] 
  </i class="+ topic> 
 </i class="+ topic> 
</i class="+ topic>
```

* `source`  — 要加密的文件的名称。
* `dest`  — 生成的加密文件的名称。

   如果指定目录，则加密文件将自动保存在指定的目录中，其文件名与指定作为源文件的文件名相同。 但是，不能指定包含源文件的目标目录。

**使用同一密钥封装多个文件** （用于多比特率支持）：

```
java -jar AdobePackager.jar  
<i class="+ topic ph hi-d="" i "="">
  sourcefiles  
 <i class="+ topic ph hi-d="" i "="">
   dest-directory [ 
  <i class="+ topic ph hi-d="" i "="">
    options] 
  </i class="+ topic> 
 </i class="+ topic> 
</i class="+ topic>
```

* `sourcefiles`  — 要加密的文件的一系列以空格分隔的源条目。
* `dest-directory`  — 要写入加密内容的目标目录。 加密文件将自动保存在此目录中，使用与源文件相同的文件名。 但是，目标目录不能包含任何源文件。

**查看有关加密文件的信息：**

```
java -jar AdobePackager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  encryptedfile [-e] [-m] 
</i class="+ topic>
```

**查看有关元数据文件的信息：**

```
java -jar AdobePackager.jar -dm <metadatafile> [-e]
```

* `metadatafile` 是 [!DNL .metadata] 包含DRM元数据的文件。

>[!NOTE]
>
>在打包过程中，媒体打包程序无法再生成 [!DNL .header] 默认文件。 要生成 [!DNL .header] 文件，使用 `-h` 选项。

**表3：选项**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_wgz_spy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">命令行选项 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">描述 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-c <span class="+ topic/ph pr-d/codeph codeph"> 配置文件 </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定配置文件的名称和位置。 </p> <p class="- topic/p ">如果未指定名称或位置，则DRM Media Packager将搜索 <span class="filepath"> flashaccesstools.properties </span> 在当前工作目录中。 </p> <p>注意：在命令行中指定的选项优先于在配置文件中指定的选项。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <span class="+ topic/ph pr-d/codeph codeph"> encryptedfile </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">用于查看有关已打包的文件的信息。 </p> <p class="- topic/p ">源文件和目标文件不是必需的。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-dm <span class="+ topic/ph pr-d/codeph codeph"> 元数据文件 </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">用于查看有关现有元数据的信息。 </p> <p class="- topic/p ">源文件和目标文件不是必需的。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-e </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">在将此选项与 <span class="codeph"> -d </span> 选项。 </p> <p class="- topic/p ">在加密文件所在的同一目录中自动创建一个文件，该文件具有文件名和DRM策略标识符。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-h </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">在将此选项与 <span class="codeph"> -d </span> 选项。 </p> <p class="- topic/p ">在加密文件所在的同一目录中自动创建一个文件，该文件名和扩展名相同 <span class="filepath"> .header </span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-i <span class="+ topic/ph pr-d/codeph codeph"> contentid </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">为此内容区段指定唯一标识符。 </p> <p class="- topic/p ">如果不指定标识符，则会自动应用destfile文件名。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-k <span class="+ topic/ph pr-d/codeph codeph"> 键 </span>= <span class="+ topic/ph pr-d/codeph codeph"> 值 </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定要添加到内容元数据的自定义键/值。 </p> <p class="- topic/p ">您可以指定多个 <span class="codeph"> -k </span> 选项。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-m </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">在将此选项与一起应用时，从打包的文件中提取元数据 <span class="codeph"> -d </span> 选项。 </p> <p class="- topic/p ">文件自动创建在与加密文件相同的目录中，并带有文件名和 <span class="codeph"> .metadata </span> 扩展。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-noprompt </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">不要询问是否应覆盖目标文件。 </p> <p class="- topic/p ">如果目标文件已存在，并且 <span class="codeph"> -o </span> 未设置，则会发生错误。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-o </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">覆盖目标文件（除非目标文件已存在），而不提示您。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-p <span class="+ topic/ph pr-d/codeph codeph"> 文件名[domain-transport-cert] </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定包含DRM策略的文件名。 </p> <p class="- topic/p ">如果DRM策略要求向使用传输证书的服务器进行域注册，而服务器使用的不是您在属性文件中指定的传输证书，则需要提供域传输证书。 </p> <p class="- topic/p ">您可以指定多个 <span class="codeph"> -p </span> 选项。 默认情况下，客户端始终应用第一个选项。 您在命令行中指定的值优先于您在配置文件中指定的值。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 配置属性 {#configuration-properties}

<!--<a id="section_3081C60BE54D47569FD1E3793513A2D9"></a>-->

>[!NOTE]
>
>对于包含* n*的属性名称， *n* 表示一个整数，该整数以1开头，对于属性的每个实例都增大。

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
   <td colname="2" class="- topic/entry "> <p>指示是否加密mp4中的脚本数据。 </p> <p><i class="+ topic/ph hi-d/i ">onMetaData</i> 和 <i class="+ topic/ph hi-d/i ">onXMP</i> 即使启用此选项，脚本数据标记也永远不会加密。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.video.level</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指示视频加密级别。 </p> <p class="- topic/p ">值 <span class="codeph"> 高</span> 用于加密所有视频内容，而值 <span class="codeph"> 中</span> 和 <span class="codeph"> 低</span> 用于对包含H.264内容的mp4文件的部分视频内容进行加密。 </p> <p class="- topic/p ">值= <span class="codeph"> 高 |中 |低</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.seconds未加密</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果值大于0，则不会加密文件开头指定的内容秒数。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.asymmetric.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">用于加密密钥的许可证服务器证书文件。 </p> <p class="- topic/p ">此 <span class="codeph"> encrypt.keys.asymmetric.certfile</span> 属性指定仅包含证书的文件（可接受PEM或DER格式）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">encrypt.keys.policyFile.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">此属性可重复用于创建要应用于内容的DRM策略列表。 <span class="codeph"> n</span> 表示其值为1或更大的整数。 默认情况下，客户端使用第一个实例。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverurl</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">许可证服务器URL </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.servercert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">许可证服务器的传输证书。 </p> <p class="- topic/p ">此属性指定 <span class="filepath"> .cer</span> 仅包含证书的文件（可接受PEM或DER格式）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">包含用于签署内容的打包程序凭据的PKCS12文件。 </p> <p class="- topic/p ">此 <span class="codeph"> encrypt.sign.certfile</span> 需要参考 <span class="filepath"> .pfx</span> 包含证书和私钥的文件。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">可以应用的密码以保护由指定的文件 <span class="codeph"> encrypt.sign.certfile</span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.minServerVersion</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">设置为要打包的内容颁发许可证所需的最低服务器版本。 </p> <p class="- topic/p ">指定x（对于Primetime DRM x.0），其中x表示主要版本号。 Adobe Primetime版本3.0之前的任何服务器版本均不支持此设置。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.policyFile.n .domain.transportcert </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果DRM策略 <span class="+ topic/ph pr-d/codeph codeph"> encrypt.keys.policyFile.n</span> 要求使用支持传输证书而不是您在中指定的证书的服务器进行域注册 <span class="+ topic/ph pr-d/codeph codeph"> encrypt.license.servercert</span>，则需要提供所需的域传输证书。 </p> <p class="- topic/p ">此属性指定仅包含证书的文件（可以接受PEM或DER格式）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.licenseKey</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定许可证密钥。 </p> <p class="- topic/p ">如果不指定密钥，则会随机生成该密钥。 如果不启用密钥轮换，则可以使用此密钥加密内容。 </p> <p class="- topic/p ">启用密钥轮换时，可以使用此密钥保护轮换密钥。 密钥长度必须为16字节，并且指定为十六进制值。 十六进制值之间的空格是可选的。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.enable</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定是否启用密钥轮替。 </p> <p class="- topic/p ">如果设置为false（默认设置），则会禁用密钥轮换，并使用主控CEK来加密内容中的所有示例。 </p> <p class="- topic/p ">如果设置为true，将启用密钥轮替，并且可以使用不同的密钥加密任何内容的区段。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.rotation.key.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">启用密钥轮替后，您可以指定加密内容的轮替密钥序列。 </p> <p class="- topic/p ">如果不指定任何密钥，则会随机生成密钥。 密钥长度必须为16个字节，并指定为十六进制值。 </p> <p class="- topic/p ">十六进制值之间的空格是可选的。 <i class="+ topic/ph hi-d/i ">n</i> 必须单调递增，从1开始递增。 指定多个键时，将按照指定的顺序循环使用多个键。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.interval</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定可应用旋转密钥加密内容示例的时间间隔（以秒为单位）。 </p> <p class="- topic/p ">在经过加密内容的时间间隔后，然后应用下一个轮换密钥。 如果已启用密钥轮替，但未指定任何时间间隔，则密钥每15分钟自动轮替一次。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverless</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果此选项设置为true ，则可从其中获取许可证的许可证服务器不可用。 </p> <p class="- topic/p ">必须嵌入许可证或在带外获取许可证。 除非指定其他值，否则默认值设置为false。 只有Primetime DRM Professional支持此选项。 </p> </td> 
  </tr> 
 </tbody> 
</table>
