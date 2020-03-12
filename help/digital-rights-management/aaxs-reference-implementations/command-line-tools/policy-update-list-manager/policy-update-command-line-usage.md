---
seo-title: 命令行使用
title: 命令行使用
uuid: 1c3a450d-5d9c-4437-89dd-1bd8719268b7
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 命令行使用 {#command-line-usage}

策略更新列表管理器位于DVD的\Reference Implementation\Command Line Tools目录中。 要创建策略更新列表，请使用以下语法：

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

下表包含上述语法中所示的命令行选项的说明：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_ghb_jqy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">命令行选项 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">说明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -c配置文件 </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定配置文件的位置。 如果未使用此选项，则“策略更新列表管理器”将在工作目 <span class="filepath"> 录中查找flashaccessools. </span> properties。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "> <span class="+ topic/ph pr-d/codeph codeph"> -d文件名 </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">显示有关策略更新列表的信息。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -e日期 </span> </td> 
   <td colname="2" class="- topic/entry "> （可选）策略更新列表的到期日期。 使用格式 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd </span> 或 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd-h24:min:sec </span> （例如，2009-01-31-14:30:00表示1月31日下午2:30）。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -f文件名[certfile] </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">从现有策略更新列表添加所有条目。 只能指定一个现有文件。 </p> <p class="- topic/p ">如果此现有列表的签名凭证与用于对新列表进行签名的凭证不同，请指定其证书文件，以便验证其签名。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">请勿询问是否应覆盖目标文件。 如果目标文件已存在且 <span class="codeph"> 未设 </span> 置-o，则将返回错误。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果目标文件已存在，则覆盖它时不会提示。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -r policyID日 </span> 期“ <span class="+ topic/ph pr-d/codeph codeph"> reasonCode </span> ” " <span class="+ topic/ph pr-d/codeph codeph"> reason Text </span>" reason <span class="+ topic/ph pr-d/codeph codeph"></span><span class="+ topic/ph pr-d/codeph codeph"></span>URL" </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">（可选）在指定日期撤消策略ID。 还可以提供可选的原因代码、原因文本和原因URL。 指定空字符串“”以指示未为可选参数提供任何值。 将日期指定为 <span class="+ topic/ph pr-d/codeph codeph"> yyyy-mm-dd或 </span> yyyy-mm-dd-h24:min:sec <span class="+ topic/ph pr-d/codeph codeph"></span> (例如，2008-12-1或2008-12-1-00:00:00（2008年12月1日午夜）。 如果未指定日期，则使用当前日期。 原因代码必须大于或等于0。 可以指定多个-r选项。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-rf策略 <span class="+ topic/ph pr-d/codeph codeph"> 文件名日期 </span> “ Reason <span class="+ topic/ph pr-d/codeph codeph"> Code </span> Code " <span class="+ topic/ph pr-d/codeph codeph"> Reason Text </span>" Reason <span class="+ topic/ph pr-d/codeph codeph"></span><span class="+ topic/ph pr-d/codeph codeph"></span>URL Reason A </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">执行与-r标志相同的操作，但从给定文件中提取策略标识符。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -u策略文件名" reasonCode" " reasonText" " reasonURL" </span> </td> 
   <td colname="2" class="- topic/entry "> <p>使用给定的原因代码（可选）、原因文本（可选）和原因URL（可选），将许可证请求中的任何匹配策略替换为本策略。 </p> <p>指定空字符串“”以指示未为可选参数提供任何值。 </p> <p>原因代码必须大于或等于 <span class="codeph"> 0 </span>。 可以 <span class="codeph"> 指定多 </span> 个-u选项。 </p> </td> 
  </tr> 
 </tbody> 
</table>

