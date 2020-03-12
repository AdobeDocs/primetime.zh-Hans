---
seo-title: 命令行使用
title: 命令行使用
uuid: 72117619-a723-49d3-9aa9-5eefcf5b0916
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 命令行使用 {#command-line-usage}

要嵌入许可证，请使用以下语法：

```
    java -jar AdobeLicenseEmbedder.jar  
<i class="+ topic ph hi-d="" i "="">
  sourcefile destfile [options] 
</i class="+ topic>
```

* `sourcefile` 是加密的FLV或F4V文件。
* `destfile` 指定将写入包含嵌入式许可证的加密内容的位置。 如果指定了目录，则文件将使用与源文件相同的文件名保存在此目录中，但该目录不能是包含源文件的目录。

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
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -l license-filename </span> </td> 
   <td colname="2" class="- topic/entry "> 包含要嵌入的许可证的文件的名称。 可以 <span class="codeph"> 指定多 </span> 个-l选项来嵌入多个许可证。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="+ topic/ph pr-d/codeph codeph"> -m元数据文件名 </span> </td> 
   <td colname="2" class="- topic/entry "> 指定要为其生成许可证的内容元数据。 （需要生成许可证） </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -noprompt </span> </td> 
   <td colname="2" class="- topic/entry "> 请勿询问是否应覆盖目标文件。 如果目标文件已存在且 <span class="codeph"> 未设 </span> 置-o，则将返回错误。 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <span class="codeph"> -o </span> </td> 
   <td colname="2" class="- topic/entry "> 如果目标文件已存在，则覆盖它时不会提示。 </td> 
  </tr> 
 </tbody> 
</table>

