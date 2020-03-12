---
seo-title: 概述
title: 概述
uuid: 857390be-dd14-46c0-b8f7-2bc661c515d4
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# DRM许可证生成器 {#license-generator}

使用 [!DNL AdobeLicenseGenerator.jar] 生成许可证，而无需客户端向服务器发送许可证请求。 然后，您可以在内容中嵌入预生成的许可证，或通过其他机制（如简单的HTTP Web服务器）将许可证交付给客户端。

## License Generator命令行使用 {#license-generator-command-line-usage}

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

* `metadata` -包括Adobe Primetime DRM元数据。

   您可以使用Media Packager中的选项从受保护的 `-d -m` 内容中检索此文件。

**显示先前生成的许可证：**

```
java -jar AdobeLicenseGenerator.jar -d 
<i class="+ topic ph hi-d="" i "="">
  license
</i class="+ topic>
```

* `license` -包含由许可证生成器生成的Adobe Primetime DRM许可证。

**表6:选项**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_skr_vry_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">命令行选项 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">说明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-c配置文件</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定配置文件的名称和位置。 </p> <p class="- topic/p ">如果未指定名称或位置，DRM许可证生成器将在当前工作目录中 <span class="filepath"> 搜索flashaccessools.properties</span> 。 </p> <p>注意： 在命令行上指定的选项优先于在配置文件中指定的选项。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <i class="+ topic/ph hi-d/i "><span class="+ topic/ph pr-d/codeph codeph"> licensefile</span></i> </p> </td> 
   <td colname="2" class="- topic/entry "> 显示有关已生成许可证的信息。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-leaf leaf-filename</span> </td> 
   <td colname="2" class="- topic/entry "> 生成叶许可证并将输出保存到指定文件中。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-m元数据文件名</span> </td> 
   <td colname="2" class="- topic/entry "> 指定您需要为其生成许可证的内容元数据。 生成许可证需要此选项。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry ">请勿询问是否应覆盖目标文件。 如果目标文件已存在且 <span class="codeph"> -o</span> 尚未设置，则会发生错误。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> 如果目标文件已存在，则无需提示即可覆盖它。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-policy-policy-num</span> </td> 
   <td colname="2" class="- topic/entry "> <p>如果元数据包括多个DRM策略，则可指定用于生成许可证的DRM策略数。 </p> <p>如果不指定DRM策略的数量，则会自动应用第一个DRM策略。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-r recipient-cert</span> </td> 
   <td colname="2" class="- topic/entry ">为指定的收件人生成许可证。 您可以使用设备或域证书，并可指定多个 <span class="+ topic/ph pr-d/codeph codeph"> -r选项 </span>为多个收件人创建许可证。 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-root root-filename</span> </td> 
   <td colname="2" class="- topic/entry "> 生成根许可证并将输出保存到您指定的文件。 </td> 
  </tr> 
 </tbody> 
</table>

## 配置文件属性 {#configuration-file-properties}

在运行许可证生成器之前，您需要在配置文件中指定许可证生成器属性的值。

>[!NOTE]
>
>对于包含n的属 *性名称*, ** n表示一个以1开头的整数，并且该属性的每个实例都会增加。

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
   <td colname="2" class="- topic/entry "> <p>设置当前支持的最低客户端版本。 如果未设置此属性，则默认情况下将自动支持所有版本。 </p> <p>您可以设置此值以控制老客户如何响应他们不支持的许可证要求。 指 <span class="codeph"> 定x</span> （对于Adobe Primetime DRM x.0），其中 <span class="codeph"> x</span> 表示主要版本号。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.keyServerCert</span> </td> 
   <td colname="2" class="- topic/entry "> 密钥服务器证书，是由密钥服务器使用的Adobe颁发的许可证服务器证书。 仅当元数据/DRM策略指示密钥服务器需要用于向iOS设备交付密钥时，才应用此证书。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> PKCS12文件，其中包含用于签署许可证的许可证服务器凭据。 此属性需要引用包含证书和私钥的。pfx文件。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry ">用于保护您使用licensegen.sign.certfile选项指 <span class="+ topic/ph pr-d/codeph codeph"> 定的文件的口令</span> 。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.domainca.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p>如果生成域绑定许可证，则必须指定一个或多个域CA证书以指示许可证颁发者可以信任的域授权。 </p> <p>如果许可证接收者是域证书，而该证书不是由指定的域CA之一颁发的，则无法生成许可证。 此属性指定 <span class="filepath"> .cer</span> 文件，该文件包含PEM或DER格式的证书。 <span class="codeph">n必须</span> 单调增加，从1开始。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <lines>
     <span class="+ topic/ph pr-d/codeph codeph">licensegen.keys.ansymet. licenseServerCredential.n</span>
    </lines> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">可选的PKCS12文件，其中包含用于在元数据和DRM策略中解密CEK的附加许可证服务器凭据。 如果之前已将内容与许可证服务器证书打包在一起，而不是那些使用licensegen.sign.certfile指定的凭据，则可以配置其他凭据 <span class="codeph"></span>。 此属性需要引用包含证 <span class="filepath"> 书和私钥的</span> .pfx文件。 <span class="codeph">n必须</span> 单调增加，从1开始。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> 
    <lines>
     <span class="+ topic/ph pr-d/codeph codeph">licensegen.keys.ansymet. licenseServerCredential.n.password</span>
    </lines> </td> 
   <td colname="2" class="- topic/entry "> <p>密码用于保护您使用licensegen<span class="+ topic/ph pr-d/codeph codeph"> .keys.ansymmetric.licenseServerCredential.n属性指定的文件</span> 。 </p> </td> 
  </tr> 
 </tbody> 
</table>