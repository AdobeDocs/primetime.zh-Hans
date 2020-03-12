---
seo-title: 命令行使用
title: 命令行使用
uuid: b3a995de-653e-491a-9262-86dc56b9ce31
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 命令行使用 {#command-line-usage}

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

`metadata` 是包含Adobe Access DRM元数据的。metadata文件。 可使用Media Packager选项从受保护的内容 `-d -m` 中获取此文件。

要显示先前生成的许可证，请使用以下语法：

```
    java -jar AdobeLicenseGenerator.jar -d 
<i class="+ topic ph hi-d="" i "="">
  license
</i class="+ topic>
```

`license` 是包含由许可生成器生成的Adobe Access许可证的文件。

下表描述了可以指定的命令行选项以及前面提到的语法：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_skr_vry_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">命令行选项 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">说明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-c配置文件</span> </td> 
   <td colname="2" class="- topic/entry "> 指定配置文件的位置。 如果未使用此选项，则许可证生成器将在工作目录中查找flashaccessools.properties。 命令行上指定的选项优先于配置文件中的选项。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <i class="+ topic/ph hi-d/i "><span class="+ topic/ph pr-d/codeph codeph"> licensefile</span></i> </p> </td> 
   <td colname="2" class="- topic/entry "> 显示有关已生成许可证的信息。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-leaf leaf-filename</span> </td> 
   <td colname="2" class="- topic/entry "> 生成叶许可证并将输出写入指定文件。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-m元数据文件名</span> </td> 
   <td colname="2" class="- topic/entry "> 指定要为其生成许可证的内容元数据。 （需要生成许可证） </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -noprompt</span> </td> 
   <td colname="2" class="- topic/entry ">请勿询问是否应覆盖目标文件。 如果目标文件已存在且 <span class="codeph"> 未设置</span> -o，则将返回错误。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="codeph"> -o</span> </td> 
   <td colname="2" class="- topic/entry "> 如果目标文件已存在，则覆盖它时不会提示。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-policy-policy-num</span> </td> 
   <td colname="2" class="- topic/entry "> 如果元数据包含多个策略，请指定要使用的策略编号（从1开始）以生成许可证。 如果未指定，则使用第一个策略。 </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-r recipient-cert</span> </td> 
   <td colname="2" class="- topic/entry ">为指定的收件人生成许可证。 可以使用设备或域证书。 可以 <span class="+ topic/ph pr-d/codeph codeph"> 指定多 </span>个-r选项来为多个收件人创建许可证。 </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">-root root-filename</span> </td> 
   <td colname="2" class="- topic/entry "> 生成根许可证并将输出写入指定文件。 </td> 
  </tr> 
 </tbody> 
</table>

