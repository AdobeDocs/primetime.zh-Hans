---
seo-title: 命令行使用
title: 命令行使用
uuid: 273e9d3b-efeb-46fa-a4b1-f13247b4e498
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 命令行使用 {#command-line-usage}

“吊销列表管理器”位于DVD上的\Reference Implementation\Command Line Tools目录中。 要运行该工具，请使用以下语法之一：

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

* `destfile` 指示将写入撤销列表的位置。
* `crlNumber` 是证书撤销列表(CRL)的非负版本号。 每次更新CRL时，此编号应递增。

下表包含上述语法中所示的命令行选项的说明：

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
   <td colname="2" class="- topic/entry ">指定配置文件的位置。 如果未使用此选项，则“撤销列表管理器”将在工作目 <span class="filepath"> 录中查找flashaccessools.properties</span> 。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-d文件名</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">显示有关撤销列表的信息。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-e日期</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">（可选）撤销列表的到期日期。 使用 <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> 或 <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:sec</span> （例如，2009-01-31-14:30:00表示1月31日下午2:30）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-f文件名[certfile]</span> </td> 
   <td colname="2" class="- topic/entry ">从现有吊销列表中添加所有条目。 只能指定一个现有文件。 <p class="- topic/p ">如果此现有列表的签名凭证与用于对新列表进行签名的凭证不同，请指定其证书文件，以便验证其签名。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">请勿询问是否应覆盖目标文件。 如果目标文件已存在且未设置-o，则将返回错误。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> 如果目标文件已存在，则覆盖它时不会提示。 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-r issuerName serialNumber revocationDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">在给定日期撤消由 <span class="codeph"> issuerName</span><span class="codeph"> 和serialNumber标识</span> 的证书。 issuer <span class="codeph"> Name</span> 必须采用509名称格式(例如， <span class="codeph"> CN=12345,O=Adobe Systems Incorporated,C=US</span>)。 以十六进制格式指定序列号。 将吊销日期指定 <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> 或 <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:sec</span>，例如2008-12-1或2008-12-1-00:00:00（2008年12月1日午夜）。 如果未指定撤销日期，则使用当前日期。 </p> </td> 
  </tr> 
 </tbody> 
</table>

