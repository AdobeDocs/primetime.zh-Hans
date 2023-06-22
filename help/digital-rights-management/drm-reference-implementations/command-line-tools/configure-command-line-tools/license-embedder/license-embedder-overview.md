---
title: 概述
description: 概述
copied-description: true
exl-id: 9aebdbd0-a6f0-4c9d-be2f-a8789cadf287
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# DRM许可证嵌入程序 {#license-embedder}

使用 [!DNL AdobeLicenseEmbedder.jar] 将预生成的许可证嵌入到Media Packager保护的内容中。

## 许可证嵌入器命令行用法 {#license-embedder-command-line-usage}

```
java -jar AdobeLicenseEmbedder.jar sourcefile destfile [options]
```

* `sourcefile` 表示加密文件。
* `destfile` 指定保存带有嵌入式许可证的加密内容的文件的名称。

   如果指定目录，则文件将保存在目标目录中。 源文件的名称还将成为保存在目标目录中的文件的名称。

下表描述了您可以指定的命令行选项：

**表7：选项**

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
   <td colname="2" class="- topic/entry "> 包含要嵌入的许可证的文件名称。 您可以指定多个 <span class="codeph"> -l </span> 用于嵌入多个许可证的选项。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -m metadata-filename </span> </td> 
   <td colname="2" class="- topic/entry "> 指定可为其生成许可证的内容元数据。 需要使用此选项来生成许可证。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> 不要询问是否应该覆盖目标文件。 如果目标文件已存在，并且 <span class="codeph"> -o </span> 尚未应用，发生错误。 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> 如果目标文件已存在，则无需提示即可将其覆盖。 </td> 
  </tr> 
 </tbody> 
</table>
