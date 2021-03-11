---
title: 命令行使用
description: 命令行使用
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---


# 命令行使用{#command-line-usage}

要嵌入许可证，请使用以下语法：

```
    java -jar AdobeLicenseEmbedder.jar  
<i class="+ topic ph hi-d="" i "="">
  sourcefile destfile [options] 
</i class="+ topic>
```

* `sourcefile` 是加密的FLV或F4V文件。
* `destfile` 指定将写入包含嵌入式许可证的加密内容的位置。如果指定了目录，则文件将使用与源文件相同的文件名保存在此目录中，但该目录不得是包含源文件的目录。

下表描述了可以指定的命令行选项以及前面提到的语法：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_hnl_2sy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">命令行选项 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">说明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l许可证文件名  </span> </td> 
   <td colname="2" class="- topic/entry "> 包含要嵌入的许可证的文件的名称。 可以指定多个<span class="codeph"> -l </span>选项来嵌入多个许可证。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -m元数据文件名  </span> </td> 
   <td colname="2" class="- topic/entry "> 指定要为其生成许可证的内容元数据。 （生成许可证时需要） </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt  </span> </td> 
   <td colname="2" class="- topic/entry "> 不要询问是否应覆盖目标文件。 如果目标文件已存在且未设置<span class="codeph"> -o </span>，则将返回一个错误。 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o  </span> </td> 
   <td colname="2" class="- topic/entry "> 如果目标文件已存在，则覆盖它时不进行提示。 </td> 
  </tr> 
 </tbody> 
</table>

