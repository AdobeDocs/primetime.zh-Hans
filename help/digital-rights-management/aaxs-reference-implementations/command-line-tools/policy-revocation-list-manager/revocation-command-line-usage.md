---
seo-title: 命令行使用
title: 命令行使用
uuid: 273e9d3b-efeb-46fa-a4b1-f13247b4e498
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---


# 命令行用法{#command-line-usage}

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
* `crlNumber` 是证书吊销列表(CRL)的非负版本号。每次更新CRL时，此编号应递增。

下表包含上述语法中所示命令行选项的说明：

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
   <td colname="2" class="- topic/entry ">指定配置文件的位置。 如果未使用此选项，则吊销列表管理器将在工作目录中查找<span class="filepath"> flashaccessools.properties</span>。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-d文件名</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">显示有关吊销列表的信息。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-e日期</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">（可选）撤销列表的到期日。 使用格式<span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span>或<span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:sec</span>（例如，2009-01-31-14:30:00表示下午2:30的1月31日）。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-f文件名[certfile]</span> </td> 
   <td colname="2" class="- topic/entry ">从现有吊销列表添加所有条目。 只能指定一个现有文件。 <p class="- topic/p ">如果此现有列表的签名凭据与用于对新列表进行签名的凭据不同，则接下来请指定其证书文件，以验证其签名。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">不要询问目标文件是否应被覆盖。 如果目标文件已存在且未设置-o，则将返回错误。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> 如果目标文件已存在，则覆盖它时不进行提示。 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph">-r issuerName serialNumber revocationDate</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">在给定日期撤消由<span class="codeph"> issuerName</span>和<span class="codeph"> serialNumber</span>标识的证书。 <span class="codeph"> issuerName</span>必须采用509名称格式(例如，<span class="codeph"> CN=12345,O=Adobe Systems Incorporated,C=US</span>)。 以十六进制形式指定序列号。 将吊销日期指定为<span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd</span>或<span class="+ topic/ph pr-d/codeph codeph">yyyy-mm-dd-h24:min:sec</span>，例如2008-12-1或2008-12-00:00:00（对于12月1日午夜）08. 如果未指定吊销日期，则使用当前日期。 </p> </td> 
  </tr> 
 </tbody> 
</table>

