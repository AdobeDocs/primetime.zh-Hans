---
title: 概述
description: 概述
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---


# DRM许可证嵌入器{#license-embedder}

使用[!DNL AdobeLicenseEmbedder.jar]将预生成的许可证嵌入到Media Packager保护的内容中。

## License Embedder命令行使用{#license-embedder-command-line-usage}

```
java -jar AdobeLicenseEmbedder.jar sourcefile destfile [options]
```

* `sourcefile` 表示加密文件。
* `destfile` 指定保存包含嵌入许可证的加密内容的文件的名称。

   如果指定目录，则文件将保存在目标目录中。 源文件的名称也将成为保存在目标目录中的文件的名称。

下表介绍了可指定的命令行选项：

**表7:选项**

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
   <td colname="2" class="- topic/entry "> 指定可为其生成许可证的内容元数据。 生成许可证时需要此选项。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt  </span> </td> 
   <td colname="2" class="- topic/entry "> 不要询问是否应覆盖目标文件。 如果目标文件已存在，且<span class="codeph"> -o </span>尚未应用，则会发生错误。 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o  </span> </td> 
   <td colname="2" class="- topic/entry "> 如果目标文件已存在，则无需提示即可覆盖它。 </td> 
  </tr> 
 </tbody> 
</table>
