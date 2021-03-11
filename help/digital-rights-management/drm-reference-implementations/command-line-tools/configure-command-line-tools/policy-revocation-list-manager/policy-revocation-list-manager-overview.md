---
title: DRM吊销列表管理器
description: DRM吊销列表管理器
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---


# DRM吊销列表管理器{#policy-revocation-list-manager}

使用Primetime DRM吊销列表管理器命令行工具([!DNL AdobeRevocationListManager.jar])创建和管理吊销列表，并检查策略是否已吊销。

在运行[!DNL AdobeRevocationListManager.jar]之前，必须在配置文件的&#x200B;*策略更新列表管理器和吊销列表管理器属性*&#x200B;部分设置属性。

>[!NOTE]
>
>您还可以从命令行指定所有吊销列表管理器属性。

## 吊销列表管理器命令行使用{#revocation-list-manager-command-line-usage}

```
java -jar AdobeRevocationListManager.jar 
<i class="+ topic ph hi-d="" i "="">
 destfile 
 <i class="+ topic ph hi-d="" i "="">
  crlNumber [
  <i class="+ topic ph hi-d="" i "="">
   options] 
       java -jar AdobeRevocationListManager.jar -d 
   <i class="+ topic ph hi-d="" i "="">
     filename
   </i class="+ topic>
  </i class="+ topic>
 </i class="+ topic>
</i class="+ topic>
```

* `destfile` 指定保存吊销列表属性的文件的名称。
* `crlNumber` 表示证书吊销列表(CRL)的非负版本号。每次更新CRL时，您都需要增加此数字。

**表5:命令行选项**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_a3y_wqy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> 命令行选项 </th> 
   <th colname="2" class="- topic/entry entry"> 说明 </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-c配置文件</span> </td> 
   <td colname="2" class="- topic/entry "><p class="- topic/p ">指定配置文件的名称和位置。 </p><p class="- topic/p ">如果未指定名称或位置，DRM吊销列表管理器将在当前工作目录中搜索<span class="filepath"> flashaccessools.properties</span>。 </p><p>注意： 在命令行上指定的选项优先于在配置文件中指定的选项。 </p>指定配置文件的位置。 如果不应用此选项，吊销列表管理器将在工作目录中搜索<span class="filepath"> flashaccessools.properties</span>。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-d文件名</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">显示有关吊销列表的信息。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-e日期</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">（可选）吊销列表的过期日期。 使用以下格式之一： 
     <ul id="ul_2C89F8183C3647C593CB67576D9DED07"> 
      <li id="li_A866F6CBCB464193A119A6609C8F3B2A"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> </li> 
      <li id="li_B5F9F6C995E64464838DDE447848F707"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:sec</span> </li> 
     </ul>例如，2009-01-31-14:30:00表示1月31日下午2:30。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-f文件名[certfile]</span> </td> 
   <td colname="2" class="- topic/entry "> <p>从现有吊销列表添加所有条目。 只能指定一个现有文件。 </p> <p class="- topic/p ">如果现有列表是使用您用来签署新列表的凭据以外的凭据进行签名的，则您需要在验证其签名的旁边指定其证书文件。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">不要询问是否应覆盖目标文件。 如果目标文件已存在且未设置<span class="codeph"> -o</span>，则发生错误。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> 如果目标文件已存在，则无需提示即可覆盖它。 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-r issuerName serialNumber revocationDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">在指定日期撤消由<span class="codeph"> issuerName</span>和<span class="codeph"> serialNumber</span>标识的证书。 <span class="codeph"> issuerName</span>必须使用509名称格式。 例如，<span class="codeph"> CN=12345,O=Adobe Systems Incorporated,C=US</span>。 </p> <p>必须以十六进制格式指定序列号。 您还需要使用以下格式之一指定吊销日期： 
     <ul id="ul_1524FBC6818248F3A2B271243E649400"> 
      <li id="li_BC618EA2332D42A59B1B5434CAFFD2AF"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> </li> 
      <li id="li_97F77810D20C4CF2944EFCFF5DFAE467"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:sec</span> </li> 
     </ul>例如，2008年12月1日午夜2008-12-1或2008-12-1-00:00:00。 如果未指定吊销日期，则自动应用当前日期。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 配置属性{#configuration-properties}

您需要应用凭据来签署吊销列表。 以下吊销列表管理器属性指定一个PKCS12文件，其中包括用于签名吊销列表（许可证服务器证书）的凭据以及证书的密码：

* `revocation.sign.certfile=license-server-credentials.pfx`
* `revocation.sign.certpass=password`