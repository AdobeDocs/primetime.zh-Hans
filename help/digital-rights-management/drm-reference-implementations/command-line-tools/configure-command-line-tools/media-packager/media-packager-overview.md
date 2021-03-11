---
title: 概述
description: 概述
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 0%

---


# DRM Media Packager {#media-packager}

使用Media Packager([!DNL AdobePackager.jar])指定要应用于您的内容的DRM策略，并指定要加密的内容的哪一部分。 例如，可以指定打包程序加密视频数据，但不加密音频数据。

在运行[!DNL AdobePackager.jar]之前，必须在配置文件的Media Packager属性部分设置属性。

>[!NOTE]
>
>您还可以从命令行指定所有Media Packager属性。

## Media Packager命令行使用{#media-packager-command-line-usage}

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

   如果指定目录，则加密的文件将自动保存在指定的目录中，并使用与源文件指定的文件名相同。 但是，不能指定包含源文件的目标目录。

**使用相同的键打包多个文件** （用于多位速率支持）：

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
* `dest-directory`  — 要写入加密内容的目标目录。加密的文件将使用与源文件相同的文件名自动保存在此目录中。 但是，目标目录不能包含任何源文件。

**视图有关加密文件的信息：**

```
java -jar AdobePackager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  encryptedfile [-e] [-m] 
</i class="+ topic>
```

**视图有关元数据文件的信息：**

```
java -jar AdobePackager.jar -dm <metadatafile> [-e]
```

* `metadatafile` 是包 [!DNL .metadata] 含DRM元数据的文件。

>[!NOTE]
>
>在打包过程中，默认情况下，Media Packager不再能生成[!DNL .header]文件。 要生成[!DNL .header]文件，请在打包过程中使用`-h`选项。

**表3:选项**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_wgz_spy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">命令行选项 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">说明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-c <span class="+ topic/ph pr-d/codeph codeph"></span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定配置文件的名称和位置。 </p> <p class="- topic/p ">如果未指定名称或位置，DRM Media Packager将在当前工作目录中搜索<span class="filepath"> flashaccessools.properties </span>。 </p> <p>注意： 在命令行上指定的选项优先于在配置文件中指定的选项。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <span class="+ topic/ph pr-d/codeph codeph">加密文件</span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">使您能够视图有关已打包的文件的信息。 </p> <p class="- topic/p ">源文件和目标文件不是必需的。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-dm <span class="+ topic/ph pr-d/codeph codeph"> metadatafile </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">使您能够视图有关现有元数据的信息。 </p> <p class="- topic/p ">源文件和目标文件不是必需的。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-e </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">将此选项与<span class="codeph"> -d </span>选项结合使用时，从打包的文件中提取DRM策略。 </p> <p class="- topic/p ">在加密文件所在的同一目录中自动创建一个文件，该文件具有文件名和DRM策略标识符。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-h </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">将此选项与<span class="codeph"> -d </span>选项结合使用时，从打包的文件中提取DRM头。 </p> <p class="- topic/p ">在加密文件所在的同一目录中自动创建一个文件，其文件名和扩展名为<span class="filepath"> .header </span>。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-i <span class="+ topic/ph pr-d/codeph codeph"> contentID </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定此内容段的唯一标识符。 </p> <p class="- topic/p ">如果未指定标识符，则会自动应用目标文件名。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-k <span class="+ topic/ph pr-d/codeph codeph">键</span>= <span class="+ topic/ph pr-d/codeph codeph">值</span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定要添加到内容元数据的自定义键/值。 </p> <p class="- topic/p ">可以指定多个<span class="codeph"> -k </span>选项。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-m </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">将此选项与<span class="codeph"> -d </span>选项结合使用时，从打包的文件中提取元数据。 </p> <p class="- topic/p ">文件会自动创建在与加密文件相同的目录中，文件名为<span class="codeph"> .metadata </span>扩展名为。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-noprompt </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">不要询问是否应覆盖目标文件。 </p> <p class="- topic/p ">如果目标文件已存在且未设置<span class="codeph"> -o </span>，则会发生错误。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-o </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">在不提示您的情况下覆盖目标文件，除非它已存在。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-p <span class="+ topic/ph pr-d/codeph codeph">文件名[domain-transport-cert] </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定包含DRM策略的文件的名称。 </p> <p class="- topic/p ">如果DRM策略要求向使用传输证书而不是在属性文件中指定的传输证书的服务器进行域注册，则您需要提供域传输证书。 </p> <p class="- topic/p ">可以指定多个<span class="codeph"> -p </span>选项。 默认情况下，客户端始终应用第一个选项。 您在命令行中指定的值优先于在配置文件中指定的值。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 配置属性{#configuration-properties}

<!--<a id="section_3081C60BE54D47569FD1E3793513A2D9"></a>-->

>[!NOTE]
>
>对于包含* n*的属性名称，*n*&#x200B;表示一个整数，该整数开始为1，并且该属性的每个实例都会增加。

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
   <td colname="2" class="- topic/entry "> <p>指示是否加密mp4中的脚本数据。 </p> <p><i class="+ topic/ph hi-d/i ">即</i> 使启用 <i class="+ topic/ph hi-d/i "></i> 此选项，onMetaDat和onXMPscript数据标签也不会加密。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.video.level</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指示视频加密级别。 </p> <p class="- topic/p ">值<span class="codeph"> high</span>用于加密所有视频内容，而值<span class="codeph"> medium</span>和<span class="codeph"> low</span>用于加密包含H.264内容的mp4文件的视频内容部分。 </p> <p class="- topic/p ">值= <span class="codeph"> |中 | low</span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.contents.secondsUnencrypted</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果值大于0，则不加密文件开头指定的秒数内容。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.ansymmet.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">用于加密密钥的许可证服务器证书文件。 </p> <p class="- topic/p "><span class="codeph"> encrypt.keys.ansymetric.certfile</span>属性指定仅包含证书的文件（PEM或DER格式可接受）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">encrypt.keys.policyFile.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">此属性用于重复创建要应用于内容的DRM策略列表。 <span class="codeph"> </span> n表示值为1或更大的整数。默认情况下，客户端使用第一个实例。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverurl</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">许可证服务器URL </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.servercert</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">许可证服务器的传输证书。 </p> <p class="- topic/p ">此属性指定仅包含证书的<span class="filepath"> .cer</span>文件（PEM或DER格式可接受）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">包含用于对内容进行签名的打包程序凭据的PKCS12文件。 </p> <p class="- topic/p "><span class="codeph"> encrypt.sign.certfile</span>需要引用包含证书和私钥的<span class="filepath"> .pfx</span>文件。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">可用于保护由<span class="codeph"> encrypt.sign.certfile</span>指定的文件的口令。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.minServerVersion</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">设置为为要打包的内容颁发许可证所需的最低服务器版本。 </p> <p class="- topic/p ">指定x（对于Primetime DRM x.0），其中x表示主要发行号。 任何早于Adobe Primetime 3.0版的服务器版本都不支持此设置。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.policyFile.n .domain.transportcert  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果DRM策略<span class="+ topic/ph pr-d/codeph codeph"> encrypt.keys.policyFile.n</span>需要与支持传输证书（而不是您在<span class="+ topic/ph pr-d/codeph codeph"> encrypt.license.servercert</span>中指定的传输证书）的服务器进行域注册，则需要提供域传输证书的需要。 </p> <p class="- topic/p ">此属性指定仅包含证书的文件（PEM或DER格式可接受）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.licenseKey</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定许可证密钥。 </p> <p class="- topic/p ">如果未指定键，则会随机生成该键。 如果不启用密钥旋转，则可以使用此密钥加密内容。 </p> <p class="- topic/p ">启用键旋转时，可以使用此键保护旋转键。 密钥长度必须为16个字节，并指定为十六进制值。 十六进制值之间的空格是可选的。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.enable</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定是否启用密钥旋转。 </p> <p class="- topic/p ">如果设置为false（这是默认设置），则禁用密钥旋转，并使用主控CEK加密内容中的所有样本。 </p> <p class="- topic/p ">如果设置为true，则启用密钥旋转，并可使用不同的密钥加密任何内容的段。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">encrypt.keys.rotation.key.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">可指定在启用密钥旋转时加密内容的旋转密钥序列。 </p> <p class="- topic/p ">如果未指定任何键，则随机生成键。 键的长度必须为16字节，并指定为十六进制值。 </p> <p class="- topic/p ">十六进制值之间的空格是可选的。 <i class="+ topic/ph hi-d/i ">必</i> 须从1开始单调增加。当您指定多个键时，按您指示的顺序循环键。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.keys.rotation.interval</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定可应用旋转密钥来加密内容范例的时间间隔（以秒为单位）。 </p> <p class="- topic/p ">在经过已加密内容的时间间隔之后，然后应用下一旋转密钥。 如果已启用密钥旋转，但未指定任何时间间隔，则每15分钟自动旋转一次密钥。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> encrypt.license.serverless</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果此选项设置为true，则不提供可从中获取许可证的许可证服务器。 </p> <p class="- topic/p ">许可证必须嵌入或带外获得。 除非您指定了其他值，否则默认值设置为false。 此选项仅在Primetime DRM Professional中受支持。 </p> </td> 
  </tr> 
 </tbody> 
</table>