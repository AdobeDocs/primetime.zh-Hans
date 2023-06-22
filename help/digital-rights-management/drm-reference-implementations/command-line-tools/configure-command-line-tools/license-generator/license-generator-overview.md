---
title: 概述
description: 概述
copied-description: true
exl-id: ba6e8fab-b199-4969-b372-06fa6d7a1e4a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---

# DRM许可证生成器 {#license-generator}

使用 [!DNL AdobeLicenseGenerator.jar] 生成许可证，而不要求客户端向服务器发送许可证请求。 然后，您可以在内容中嵌入预生成的许可证，或通过其他机制（如简单的HTTP Web服务器）将许可证交付给客户端。

## 许可证生成器命令行用法 {#license-generator-command-line-usage}

**生成许可证：**

```
java -jar AdobeLicenseGenerator.jar -m 
<i class="+ topic ph hi-d="" i "="">
 metadata 
 <i class="+ topic ph hi-d="" i "="">
   [options]
 </i class="+ topic>
</i class="+ topic>
```

* `metadata`  — 包含Adobe Primetime DRM元数据。

   您可以使用从受保护内容中检索此文件 `-d -m` 选项。

**显示以前生成的许可证：**

```
java -jar AdobeLicenseGenerator.jar -d 
<i class="+ topic ph hi-d="" i "="">
  license
</i class="+ topic>
```

* `license`  — 包含由许可证生成器生成的Adobe Primetime DRM许可证。

**表6：选项**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_skr_vry_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">命令行选项 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">描述 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-c配置文件</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定配置文件的名称和位置。 </p> <p class="- topic/p ">如果未指定名称或位置，则“DRM许可证生成器”将搜索 <span class="filepath"> flashaccesstools.properties</span> 在当前工作目录中。 </p> <p>注意：在命令行中指定的选项优先于在配置文件中指定的选项。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <i class="+ topic/ph hi-d/i "><span class="+ topic/ph pr-d/codeph codeph"> licensefile</span></i> </p> </td> 
   <td colname="2" class="- topic/entry "> 显示有关已生成的许可证的信息。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-leaf叶文件名</span> </td> 
   <td colname="2" class="- topic/entry "> 生成叶许可证并将输出保存在指定的文件中。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-m metadata-filename</span> </td> 
   <td colname="2" class="- topic/entry "> 指定需要为其生成许可证的内容元数据。 需要使用此选项来生成许可证。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry ">不要询问是否应该覆盖目标文件。 如果目标文件已存在，并且 <span class="codeph"> -o</span> 尚未设置，发生错误。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> 如果目标文件已存在，则无需提示即可将其覆盖。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-policy policy policy-num</span> </td> 
   <td colname="2" class="- topic/entry "> <p>如果元数据包括多个DRM策略，则可以指定可用于生成许可证的DRM策略数量。 </p> <p>如果不指定DRM策略的数目，则自动应用第一个DRM策略。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-r recipient-cer</span> </td> 
   <td colname="2" class="- topic/entry ">为指定的收件人生成许可证。 您可以使用设备或域证书，并且可以指定多个 <span class="+ topic/ph pr-d/codeph codeph"> -r </span>选项来为多个收件人创建许可证。 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-root-filename</span> </td> 
   <td colname="2" class="- topic/entry "> 生成根许可证并将输出保存到指定的文件中。 </td> 
  </tr> 
 </tbody> 
</table>

## 配置文件属性 {#configuration-file-properties}

在运行许可证生成器之前，需要为配置文件中的许可证生成器属性指定值。

>[!NOTE]
>
>对于包含的属性名称 *n*， *n* 表示一个整数，该整数以1开头，对于属性的每个实例都增大。

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
   <td colname="2" class="- topic/entry "> <p>设置当前支持的最低客户端版本。 如果不设置此属性，则默认情况下自动支持所有版本。 </p> <p>您可以设置此值来控制旧版客户端如何响应它们不支持的许可证要求。 指定 <span class="codeph"> x</span> (适用于Adobe Primetime DRM x.0)，其中 <span class="codeph"> x</span> 表示主要版本号。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.keyServerCert</span> </td> 
   <td colname="2" class="- topic/entry "> Key Server证书，这是Key Server使用的Adobe颁发的License Server证书。 仅当元数据/DRM策略指示需要密钥服务器才能将密钥交付到iOS设备时，才应用此证书。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> 包含用于签署许可证的许可证服务器凭据的PKCS12文件。 此属性需要引用包含证书和私钥的.pfx文件。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry ">用于保护指定文件的密码 <span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certfile</span> 选项。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.domainca.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p>如果您生成绑定域的许可证，则必须指定一个或多个域CA证书，以指示许可证颁发者可以信任的域颁发机构。 </p> <p>如果许可证收件人是由指定的域CA之一颁发的域证书，则无法生成许可证。 此属性指定 <span class="filepath"> .cer</span> 包含PEM或DER格式证书的文件。 <span class="codeph">n</span> 必须从1开始单调增加。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <code>licensegen.keys.asymmetric. licenseServerCredential.n</code>
   </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">可选的PKCS12文件，该文件包含用于解密元数据和DRM策略中的CEK的附加许可证服务器凭据。 如果内容先前已打包有许可证服务器证书，而不是那些已指定的凭据，则可以配置其他凭据 <span class="codeph"> licensegen.sign.certfile</span>. 此属性需要引用 <span class="filepath"> .pfx</span> 包含证书和私钥的文件。 <span class="codeph">n</span> 必须从1开始单调增加。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <code>licensegen.keys.asymmetric. licenseServerCredential.n.password</code>
   </td> 
   <td colname="2" class="- topic/entry "> <p>应用密码以保护您使用指定的文件<span class="+ topic/ph pr-d/codeph codeph"> licensegen.keys.asymmetric.licenseServerCredential.n</span> 属性。 </p> </td> 
  </tr> 
 </tbody> 
</table>
