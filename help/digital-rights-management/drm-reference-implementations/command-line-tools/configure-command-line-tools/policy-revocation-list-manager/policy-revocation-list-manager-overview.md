---
title: DRM吊销列表管理器
description: DRM吊销列表管理器
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 0%

---

# DRM吊销列表管理器 {#policy-revocation-list-manager}

使用Primetime DRM吊销列表管理器命令行工具( [!DNL AdobeRevocationListManager.jar])，以创建和管理吊销列表，并检查策略是否已吊销。

运行之前 [!DNL AdobeRevocationListManager.jar]，您必须在以下位置设置属性： *策略更新列表管理器和吊销列表管理器属性* 部分。

>[!NOTE]
>
>您还可以从命令行指定所有“吊销列表管理器”属性。

## 吊销列表管理器命令行用法 {#revocation-list-manager-command-line-usage}

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
* `crlNumber` 表示证书吊销列表(CRL)的非负版本号。 每次更新CRL时，您需要递增此数字。

**表5：命令行选项**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_a3y_wqy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> 命令行选项 </th> 
   <th colname="2" class="- topic/entry entry"> 描述 </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-c配置文件</span> </td> 
   <td colname="2" class="- topic/entry "><p class="- topic/p ">指定配置文件的名称和位置。 </p><p class="- topic/p ">如果未指定名称或位置，则“DRM吊销列表管理器”将搜索 <span class="filepath"> flashaccesstools.properties</span> 在当前工作目录中。 </p><p>注意：在命令行中指定的选项优先于在配置文件中指定的选项。 </p>指定配置文件的位置。 如果不应用此选项，“吊销列表管理器”将搜索 <span class="filepath"> flashaccesstools.properties</span> 在工作目录中。 </td> 
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
      <li id="li_B5F9F6C995E64464838DDE447848F707"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:秒</span> </li> 
     </ul>例如，2009-01-31-14:30:00代表1月31日下午2:30。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-f文件名[certfile]</span> </td> 
   <td colname="2" class="- topic/entry "> <p>从现有吊销列表中添加所有条目。 您只能指定一个现有文件。 </p> <p class="- topic/p ">如果现有列表是使用用于为新列表签名的凭据以外的凭据进行签名，则需要指定其证书文件以验证其签名。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">不要询问是否应覆盖目标文件。 如果目标文件已存在，并且 <span class="codeph"> -o</span> 未设置，则会发生错误。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> 如果目标文件已存在，则无需提示即可将其覆盖。 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-r issuerName serialNumber吊销日期</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">撤销已识别的证书 <span class="codeph"> issuerName</span> 和 <span class="codeph"> 序列号</span> 指定日期。 此 <span class="codeph"> issuerName</span> 必须使用509名称格式。 例如， <span class="codeph"> CN=12345，O=Adobe Systems Incorporated，C=US</span>. </p> <p>必须以十六进制格式指定序列号。 您还需要以下列格式之一指定撤销日期： 
     <ul id="ul_1524FBC6818248F3A2B271243E649400"> 
      <li id="li_BC618EA2332D42A59B1B5434CAFFD2AF"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> </li> 
      <li id="li_97F77810D20C4CF2944EFCFF5DFAE467"><span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:秒</span> </li> 
     </ul>例如，2008-12-1或2008-12-1-00:00:2008年12月1日午夜00。 如果未指定撤消日期，则自动应用当前日期。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 配置属性 {#configuration-properties}

您需要将凭据应用于签名吊销列表。 以下吊销列表管理器属性指定一个PKCS12文件，其中包含签名吊销列表的凭据（许可证服务器证书）以及证书的密码：

* `revocation.sign.certfile=license-server-credentials.pfx`
* `revocation.sign.certpass=password`
