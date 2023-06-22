---
title: 命令行用法
description: 命令行用法
copied-description: true
exl-id: 51b11ef8-438e-4747-be3e-e1774dc9f31a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# 命令行用法 {#command-line-usage}

要嵌入许可证，请使用以下语法：

```
    java -jar AdobeLicenseEmbedder.jar  
<i class="+ topic ph hi-d="" i "="">
  sourcefile destfile [options] 
</i class="+ topic>
```

* `sourcefile` 是一个加密的FLV或F4V文件。
* `destfile` 指定将写入具有嵌入式许可证的加密内容的位置。 如果指定了目录，则文件将使用与源文件相同的文件名保存在此目录中，但该目录不能是包含源文件的目录。

下表描述了可与前面提到的语法一起指定的命令行选项：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_hnl_2sy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">命令行选项 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">描述 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l license-filename </span> </td> 
   <td colname="2" class="- topic/entry "> 包含要嵌入的许可证的文件名称。 多个 <span class="codeph"> -l </span> 可以指定嵌入多个许可证的选项。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -m metadata-filename </span> </td> 
   <td colname="2" class="- topic/entry "> 指定要为其生成许可证的内容元数据。 （需要生成许可证） </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> 不要询问是否应该覆盖目标文件。 如果目标文件已存在，并且 <span class="codeph"> -o </span> 未设置，将返回错误。 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> 如果目标文件已存在，则无需提示即可将其覆盖。 </td> 
  </tr> 
 </tbody> 
</table>
