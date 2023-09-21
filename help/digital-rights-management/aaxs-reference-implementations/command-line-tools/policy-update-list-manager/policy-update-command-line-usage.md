---
title: 命令行用法
description: 命令行用法
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# 命令行用法 {#command-line-usage}

策略更新列表管理器位于DVD上的\Reference Implementation\Command Line Tools目录中。 要创建策略更新列表，请使用以下语法：

```
    java -jar AdobePolicyUpdateListManager.jar  
<i class="+ topic ph hi-d="" i "="">
  destfile [ 
 <i class="+ topic ph hi-d="" i "="">
   options]  
 </i class="+ topic> 
</i class="+ topic>
```

* `destfile` 指示将写入策略更新列表的位置。

要查看现有策略更新列表，请使用以下语法：

```
    java -jar AdobePolicyUpdateListManager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  filename 
</i class="+ topic>
```

下表包含上述语法中所示的命令行选项说明：

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定配置文件的位置。 如果未使用此选项，则策略更新列表管理器将查找 <span class="filepath"> flashaccesstools.properties </span> 在工作目录中。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -d文件名 </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">显示有关策略更新列表的信息。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e日期 </span> </td> 
   <td colname="2" class="- topic/entry "> （可选）策略更新列表的到期日期。 使用格式 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> 或 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:秒 </span> (例如，2009-01-31-14:30:00表示1月31日下午2:30)。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -f文件名[certfile] </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">从现有策略更新列表中添加所有条目。 只能指定一个现有文件。 </p> <p class="- topic/p ">如果此现有列表使用与用于为新列表签名的凭据不同的凭据进行签名，请指定其证书文件，以便可以验证其签名。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">不要询问是否应覆盖目标文件。 如果目标文件已存在，并且 <span class="codeph"> -o </span> 未设置，将返回错误。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果目标文件已存在，则在不提示的情况下将其覆盖。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r policyID </span> <span class="+ topic/ph pr-d/codeph codeph"> 日期 </span> " <span class="+ topic/ph pr-d/codeph codeph"> 原因代码 </span>“ ” <span class="+ topic/ph pr-d/codeph codeph"> 原因文本 </span>“ ” <span class="+ topic/ph pr-d/codeph codeph"> reasonURL </span>" </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">（可选）在指定日期撤销策略ID。 可能还会提供可选的原因代码、原因文本和原因URL。 指定空字符串“”以指示没有为可选参数提供值。 指定日期为 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> 或 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:秒 </span> (例如2008-12-1或2008-12-1-00:00:2008年12月1日午夜)。 如果未指定日期，则使用当前日期。 原因代码必须大于或等于0。 可以指定多个 — r选项。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-rf <span class="+ topic/ph pr-d/codeph codeph"> policyFilename </span> <span class="+ topic/ph pr-d/codeph codeph"> 日期 </span> " <span class="+ topic/ph pr-d/codeph codeph"> 原因代码 </span>“ ” <span class="+ topic/ph pr-d/codeph codeph"> 原因文本 </span>“ ” <span class="+ topic/ph pr-d/codeph codeph"> reasonURL </span>" </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">执行与 — r标志相同的操作，但会从给定文件中提取策略标识符。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -u policyFilename " reasonCode" " reasonText" " reasonURL" </span> </td> 
   <td colname="2" class="- topic/entry "> <p>使用给定原因代码（可选）、原因文本（可选）和原因URL（可选）将许可证请求中的任何匹配策略替换为此策略。 </p> <p>指定空字符串“”以指示没有为可选参数提供值。 </p> <p>原因代码必须大于或等于 <span class="codeph"> 0 </span>. 多个 <span class="codeph"> -u </span> 可以指定选项。 </p> </td> 
  </tr> 
 </tbody> 
</table>
