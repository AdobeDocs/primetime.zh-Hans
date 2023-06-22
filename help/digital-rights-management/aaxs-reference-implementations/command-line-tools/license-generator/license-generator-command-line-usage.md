---
title: 命令行用法
description: 命令行用法
copied-description: true
exl-id: 241849bb-e818-420e-98b4-c12e306b17b2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# 命令行用法 {#command-line-usage}

要生成许可证，请使用以下语法：

```
    java -jar AdobeLicenseGenerator.jar -m 
<i class="+ topic ph hi-d="" i "="">
 metadata 
 <i class="+ topic ph hi-d="" i "="">
   [options]
 </i class="+ topic>
</i class="+ topic>
```

`metadata` 是一个包含Adobe访问DRM元数据的.metadata文件。 可使用从受保护内容中获取此文件 `-d -m` 选项。

要显示以前生成的许可证，请使用以下语法：

```
    java -jar AdobeLicenseGenerator.jar -d 
<i class="+ topic ph hi-d="" i "="">
  license
</i class="+ topic>
```

`license` 是一个文件，其中包含许可证生成器生成的Adobe访问许可证。

下表描述了可与前面提到的语法一起指定的命令行选项：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_skr_vry_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">命令行选项 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">描述 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-c配置文件</span> </td> 
   <td colname="2" class="- topic/entry "> 指定配置文件的位置。 如果不使用此选项，许可证生成器将在工作目录中查找flashaccesstools.properties。 在命令行中指定的选项优先于配置文件中的选项。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <i class="+ topic/ph hi-d/i "><span class="+ topic/ph pr-d/codeph codeph"> licensefile</span></i> </p> </td> 
   <td colname="2" class="- topic/entry "> 显示有关已生成的许可证的信息。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-leaf叶文件名</span> </td> 
   <td colname="2" class="- topic/entry "> 生成叶许可证并将输出写入指定的文件。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-m metadata-filename</span> </td> 
   <td colname="2" class="- topic/entry "> 指定要为其生成许可证的内容元数据。 （需要生成许可证） </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry ">不要询问是否应该覆盖目标文件。 如果目标文件已存在，并且 <span class="codeph"> -o</span> 未设置，将返回错误。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> 如果目标文件已存在，则无需提示即可将其覆盖。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-policy policy policy-num</span> </td> 
   <td colname="2" class="- topic/entry "> 如果元数据包含多个策略，请指定要用于生成许可证的策略的编号（从1开始）。 如果未指定，则使用第一个策略。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-r recipient-cer</span> </td> 
   <td colname="2" class="- topic/entry ">为指定的收件人生成许可证。 可以使用设备或域证书。 多个 <span class="+ topic/ph pr-d/codeph codeph"> -r </span>可以指定选项来为多个收件人创建许可证。 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-root-filename</span> </td> 
   <td colname="2" class="- topic/entry "> 生成根许可证并将输出写入指定的文件。 </td> 
  </tr> 
 </tbody> 
</table>
