---
title: 概述
description: 概述
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 0%

---


# DRM策略更新列表管理器{#policy-update-list-manager}

使用Primetime DRM策略更新列表管理器命令行工具([!DNL AdobePolicyUpdateListManager.jar])可创建和管理DRM策略更新列表，并检查策略是否已更新或吊销。

在运行策略更新列表管理器命令行工具之前，必须在配置文件的&#x200B;*策略更新列表管理器和吊销列表管理器属性*&#x200B;部分中设置属性。

>[!NOTE]
>
>您还可以从命令行指定所有策略更新列表管理器属性。

## 策略更新列表管理器命令行使用{#policy-update-list-manager-command-line-usage}

**创建策略更新列表:**

```
java -jar AdobePolicyUpdateListManager.jar  
<i class="+ topic ph hi-d="" i "="">
  destfile [ 
 <i class="+ topic ph hi-d="" i "="">
   options]  
 </i class="+ topic> 
</i class="+ topic>
```

* `destfile` 指示写入DRM策略更新列表的文件的名称。

**视图现有策略更新列表:**

```
java -jar AdobePolicyUpdateListManager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  filename 
</i class="+ topic>
```

* `filename` 策略更新列表文件的名称。

**表4:命令行选项**

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_ghb_jqy_n4">  
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">命令行选项 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">说明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c配置文件  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定配置文件的名称和位置。 </p> <p class="- topic/p ">如果未指定名称或位置，则DRM策略更新列表管理器将搜索当前工作目录中的<span class="filepath"> flashaccessools.properties </span>。 </p> <p>注意： 在命令行上指定的选项优先于在配置文件中指定的选项。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -d文件名  </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">显示有关DRM策略更新列表的信息。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e日期  </span> </td> 
   <td colname="2" class="- topic/entry "> <p>（可选）DRM策略更新列表的到期日期。 </p> <p>使用格式<span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span>或<span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:sec </span>(例如，2009-01-31-14:30:00表示1月31日下午2:30)。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -f文件名[certfile]  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">从现有DRM策略更新列表添加所有条目。 只能指定一个现有文件。 </p> <p class="- topic/p ">如果现有列表已使用除用于对新列表进行签名的凭据之外的凭据进行签名，则您需要指定其证书文件以验证其签名。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -noprompt  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">不要询问是否应覆盖目标文件。 如果目标文件已存在且未设置<span class="codeph"> -o </span>，则会发生错误。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o  </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果目标文件已存在，则覆盖它时不进行提示。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r policyID  </span> <span class="+ topic/ph pr-d/codeph codeph"> date </span> "  <span class="+ topic/ph pr-d/codeph codeph"> reasonCode </span>" "  <span class="+ topic/ph pr-d/codeph codeph"> reasonText"  </span>"  <span class="+ topic/ph pr-d/codeph codeph">  </span>reasonURL " </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">（可选）在指定日期撤消DRM策略ID。 您可以提供可选的原因代码、原因文本和原因URL。 您需要指定空字符串""以指示未为可选参数提供任何值。 您可以在<span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span>或<span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:sec </span>中指定日期。 例如，2008-12-1或2008-12-1-00:00:00表示2008年12月1日午夜)。 如果未指定日期，则会自动应用当前日期。 因此，原因代码必须大于或等于0。 您还可以指定多个 — r选项。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-rf <span class="+ topic/ph pr-d/codeph codeph">策略文件名</span> <span class="+ topic/ph pr-d/codeph codeph"> date </span> " <span class="+ topic/ph pr-d/codeph codeph"> reasonCode </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonText </span>" " <span class="+ topic/ph pr-d/codeph codeph"> reasonURL </span>" </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">执行与<span class="codeph"> -r </span>选项相同的操作。 但是，它会从指定文件中提取DRM策略标识符。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -u policyFilename " reasonCode" " reasonText" "reasonURL"  </span> </td> 
   <td colname="2" class="- topic/entry "> <p>使用给定的原因代码（可选）、原因文本（可选）和原因URL（可选），将许可证请求中的任何匹配DRM策略替换为此DRM策略。 </p> <p>空字符串“”表示您没有为可选参数提供任何值。 </p> <p>原因代码必须大于或等于<span class="codeph"> 0 </span>。 可以指定多个<span class="codeph"> -u </span>选项。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 配置属性{#configuration-properties}

以下Primetime DRM策略更新列表管理器属性指定PKCS12文件，该文件包括签名吊销列表（许可证服务器证书）的凭据和密码。

* `revocation.sign.certfile=license-server-credentials.pfx`
* `revocation.sign.certpass=password`