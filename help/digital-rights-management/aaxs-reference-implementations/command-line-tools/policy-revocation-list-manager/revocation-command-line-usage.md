---
title: 命令行用法
description: 命令行用法
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# 命令行用法 {#command-line-usage}

吊销列表管理器位于DVD的\Reference Implementation\Command Line Tools目录中。 要运行该工具，请使用以下语法之一：

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

* `destfile` 指示将写入吊销列表的位置。
* `crlNumber` 是证书吊销列表(CRL)的非负版本号。 每次更新CRL时，此数量都应增加。

下表包含上述语法中所示的命令行选项说明：

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
   <td colname="2" class="- topic/entry ">指定配置文件的位置。 如果未使用此选项，吊销列表管理器将查找 <span class="filepath"> flashaccesstools.properties</span> 在工作目录中。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-d文件名</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">显示有关吊销列表的信息。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-e日期</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">（可选）吊销列表的过期日期。 使用格式 <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> 或 <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:秒</span> (例如，2009-01-31-14:30:00表示1月31日下午2:30)。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-f文件名[certfile]</span> </td> 
   <td colname="2" class="- topic/entry ">从现有吊销列表中添加所有条目。 只能指定一个现有文件。 <p class="- topic/p ">如果此现有列表使用与用于为新列表签名的凭据不同的凭据进行签名，则接下来指定其证书文件，以便可以验证其签名。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">不要询问是否应覆盖目标文件。 如果目标文件已存在，但未设置 — o ，则会返回错误。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> 如果目标文件已存在，则在不提示的情况下将其覆盖。 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-r issuerName serialNumber吊销日期</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">吊销由标识的证书 <span class="codeph"> issuerName</span> 和 <span class="codeph"> 序列号</span> 在给定的日期。 此 <span class="codeph"> issuerName</span> 必须遵循509名称格式(例如， <span class="codeph"> CN=12345，O=Adobe Systems Incorporated，C=US</span>)。 以十六进制格式指定序列号。 将吊销日期指定为 <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span> 或 <span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:秒</span>，例如2008-12-1或2008-12-1-00:00:2008年12月1日午夜00。 如果未指定撤销日期，则使用当前日期。 </p> </td> 
  </tr> 
 </tbody> 
</table>
