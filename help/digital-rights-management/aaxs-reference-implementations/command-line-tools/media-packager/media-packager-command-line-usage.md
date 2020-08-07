---
seo-title: 命令行使用
title: 命令行使用
uuid: 5f24f18d-09ef-400a-9404-50a9fcf4316d
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---


# 命令行使用 {#command-line-usage}

在使用Media Packager之前，请确保满足“要求”中列出的要求，并且配置文件包含所需信息(请参阅“使用Adobe访问参考 *实现”中的配置文件*。

Media Packager位于DVD [!DNL \Reference Implementation\Command Line tools] 上的目录中。 要加密单个文件，请使用以下语法：

```
java -jar AdobePackager.jar  
<i class="+ topic ph hi-d="" i "="">
  source  
 <i class="+ topic ph hi-d="" i "="">
   dest [ 
  <i class="+ topic ph hi-d="" i "="">
    options] 
  </i class="+ topic> 
 </i class="+ topic> 
</i class="+ topic>
```

* `source` 是要加密的文件。
* `dest` 指定加密内容的写入位置。 如果指定了目录，则加密文件将使用与源文件相同的文件名保存在此文件夹中，但该目录不能是包含源文件的目录。

要使用相同的密钥加密多个文件（用于多比特率支持），请使用以下语法：

```
java -jar AdobePackager.jar  
<i class="+ topic ph hi-d="" i "="">
  sourcefiles  
 <i class="+ topic ph hi-d="" i "="">
   dest-directory [ 
  <i class="+ topic ph hi-d="" i "="">
    options] 
  </i class="+ topic> 
 </i class="+ topic> 
</i class="+ topic>
```

* `sourcefiles` 是一系列以空格分隔的源条目，它们表示要加密的文件。
* `dest-directory` 指定加密内容的写入位置。 加密的文件将使用与源文件相同的文件名保存在此文件夹中，但目录不能是包含源文件的目录。

要视图有关已加密文件的信息，请使用以下语法：

```
java -jar AdobePackager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  encryptedfile [-e] [-m] 
</i class="+ topic>
```

* `encryptedfile` 是加密文件。

要视图有关元数据文件的信息，请使用以下语法：

```
java -jar AdobePackager.jar -dm <metadatafile> [-e]
```

* `metadatafile` 是包 [!DNL .metadata] 含DRM元数据的文件。

>[!NOTE]
>
>在打包过程中，默认情况下，Media Packager不再生成。header文件。 要生成此文件，请在打包 `-h` 过程中使用选项。

下表包含上述语法中所示命令行选项的说明：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_wgz_spy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">命令行选项 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">说明 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-c <span class="+ topic/ph pr-d/codeph codeph"> configfile </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定配置文件的位置。 如果未使用此选项，Media Packager将在工作目 <span class="filepath"> 录中查找 </span> flashaccessols.properties。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d已加 <span class="+ topic/ph pr-d/codeph codeph"> 密文件 </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">显示有关已打包文件的信息。 源文件和目标文件不是必需的。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-dm <span class="+ topic/ph pr-d/codeph codeph"> metadatafile </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">显示有关现有元数据的信息。 源文件和目标文件不是必需的。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-e </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">将此选项与-d <span class="codeph"> 结合使 </span> 用，从打包的文件中提取策略。 将使用文件名和策略标识符在与加密文件相同的目录中创建文件。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-h </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">与- <span class="codeph"> d一起 </span> 使用，从打包的文件中提取DRM头。 使用文件名和扩展名。header在与加密文件相同的目录中创建文 <span class="filepath"> 件 </span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-i <span class="+ topic/ph pr-d/codeph codeph"> contentID </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定此内容段的唯一标识符。 如果未指定标识符，则将使用目标文件名。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-k <span class="+ topic/ph pr-d/codeph codeph"> 键 </span>= <span class="+ topic/ph pr-d/codeph codeph"> 值 </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定要添加到内容元数据的自定义键／值。 可以 <span class="codeph"> 指定 </span> 多个-k选项。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-m </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">将此选项与-d <span class="codeph"> 结合使 </span> 用，从打包的文件中提取元数据。 将使用文件名和扩展名。metadata在与加密文件相同的目录中创建 <span class="codeph"> 文件 </span>。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-noprompt </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">不要询问是否应覆盖目标文件。 如果目标文件已存在 <span class="codeph"> 且 </span> 未设置-o，则将返回错误。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-o </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">覆盖目标文件（如果它已存在），但不进行提示。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-p文 <span class="+ topic/ph pr-d/codeph codeph"> 件名[domain-transport-cert] </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定包含策略的文件的名称。 如果策略要求向使用与属性文件中指定的传输证书不同的传输证书的服务器进行域注册，则还需要提供域传输证书。 </p> <p class="- topic/p ">可 <span class="codeph"> 以指 </span> 定多个-p选项，默认情况下，客户端将使用第一个选项。 在命令行上指定的值优先于在配置文件中指定的值。 </p> </td> 
  </tr> 
 </tbody> 
</table>

