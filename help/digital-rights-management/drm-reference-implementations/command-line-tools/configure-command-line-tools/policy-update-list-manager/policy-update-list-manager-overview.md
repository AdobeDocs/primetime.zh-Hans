---
title: 概述
description: 概述
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---

# DRM策略更新列表管理器 {#policy-update-list-manager}

使用Primetime DRM策略更新列表管理器命令行工具( [!DNL AdobePolicyUpdateListManager.jar])，以创建和管理DRM策略更新列表，并检查是否已更新或撤消策略。

运行Policy Update List Manager命令行工具之前，必须在 *策略更新列表管理器和吊销列表管理器属性* 部分。

>[!NOTE]
>
>您还可以从命令行指定所有“策略更新列表管理器”属性。

## 策略更新列表管理器命令行用法 {#policy-update-list-manager-command-line-usage}

**创建策略更新列表：**

```
java -jar AdobePolicyUpdateListManager.jar  
<i class="+ topic ph hi-d="" i "="">
  destfile [ 
 <i class="+ topic ph hi-d="" i "="">
   options]  
 </i class="+ topic> 
</i class="+ topic>
```

* `destfile` 指示写入DRM策略更新列表的文件名。

**查看现有策略更新列表：**

```
java -jar AdobePolicyUpdateListManager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  filename 
</i class="+ topic>
```

* `filename` 策略更新列表文件的名称。

**表4：命令行选项**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_ghb_jqy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">命令行选项 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">描述 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c配置文件 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定配置文件的名称和位置。 </p> <p class="- topic/p ">如果未指定名称或位置，则DRM策略更新列表管理器将搜索 <span class="filepath"> flashaccesstools.properties </span> 在当前工作目录中。 </p> <p>注意：在命令行中指定的选项优先于在配置文件中指定的选项。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -d文件名 </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">显示有关DRM策略更新列表的信息。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e日期 </span> </td> 
   <td colname="2" class="- topic/entry "> <p>（可选）DRM策略更新列表的到期日期。 </p> <p>使用格式 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> 或 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:秒 </span> (例如，2009-01-31-14:30:00表示1月31日下午2:30)。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -f文件名[certfile] </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">从现有DRM策略更新列表中添加所有条目。 您只能指定一个现有文件。 </p> <p class="- topic/p ">如果现有列表已使用用于为新列表签名的凭据以外的凭据进行签名，则需要指定其证书文件以验证其签名。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">不要询问是否应覆盖目标文件。 如果目标文件已存在，并且 <span class="codeph"> -o </span> 未设置，则会发生错误。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果目标文件已存在，则在不提示的情况下将其覆盖。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r policyID </span> <span class="+ topic/ph pr-d/codeph codeph"> 日期 </span> " <span class="+ topic/ph pr-d/codeph codeph"> 原因代码 </span>“ ” <span class="+ topic/ph pr-d/codeph codeph"> 原因文本 </span>“ ” <span class="+ topic/ph pr-d/codeph codeph"> reasonURL </span>" </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">（可选）在指定日期撤消DRM策略ID。 您可以提供可选的原因代码、原因文本和原因URL。 您需要指定一个空字符串“”，以指示没有为可选参数提供值。 您可以指定以下位置的日期： <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> 或 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:秒 </span> 格式进行转换。 例如，2008-12-1或2008-12-1-00:00:00表示2008年12月1日的午夜)。 如果不指定日期，则会自动应用当前日期。 因此，原因代码必须大于或等于0。 您还可以指定多个 — r选项。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-rf <span class="+ topic/ph pr-d/codeph codeph"> policyFilename </span> <span class="+ topic/ph pr-d/codeph codeph"> 日期 </span> " <span class="+ topic/ph pr-d/codeph codeph"> 原因代码 </span>“ ” <span class="+ topic/ph pr-d/codeph codeph"> 原因文本 </span>“ ” <span class="+ topic/ph pr-d/codeph codeph"> reasonURL </span>" </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">执行与相同的操作 <span class="codeph"> -r </span> 选项。 但是，它从指定的文件中提取DRM策略标识符。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -u policyFilename " reasonCode" " reasonText" " reasonURL" </span> </td> 
   <td colname="2" class="- topic/entry "> <p>使用给定原因代码（可选）、原因文本（可选）和原因URL（可选）将许可证请求中的任何匹配DRM策略替换为此DRM策略。 </p> <p>空字符串“”表示您尚未为可选参数提供任何值。 </p> <p>原因代码必须大于或等于 <span class="codeph"> 0 </span>. 您可以指定多个 <span class="codeph"> -u </span> 选项。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 配置属性 {#configuration-properties}

以下Primetime DRM策略更新列表管理器属性指定一个PKCS12文件，其中包含签名吊销列表的凭据（许可证服务器证书）以及密码。

* `revocation.sign.certfile=license-server-credentials.pfx`
* `revocation.sign.certpass=password`
