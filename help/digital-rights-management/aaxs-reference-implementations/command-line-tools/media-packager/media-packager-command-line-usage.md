---
title: 命令行使用
description: 命令行使用
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---


# 命令行使用{#command-line-usage}

在使用Media Packager之前，请确保满足“要求”中列出的要求，且配置文件包含所需信息(请参阅&#x200B;*使用Adobe访问参考实现*&#x200B;中的配置文件。

Media Packager位于DVD上的[!DNL \Reference Implementation\Command Line tools]目录中。 要加密单个文件，请使用以下语法：

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
* `dest` 指定加密内容的写入位置。如果指定了目录，则加密文件将使用与源文件相同的文件名保存在此文件夹中，但该目录不得是包含源文件的目录。

要使用相同的密钥加密多个文件（用于多位速率支持），请使用以下语法：

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

* `sourcefiles` 是一系列以空格分隔的源条目，表示要加密的文件。
* `dest-directory` 指定加密内容的写入位置。加密的文件将使用与源文件相同的文件名保存在此文件夹中，但目录不能是包含源文件的目录。

要视图有关加密文件的信息，请使用以下语法：

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
>在打包过程中，默认情况下，Media Packager将不再生成.header文件。 要生成此文件，请在打包过程中使用`-h`选项。

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
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-c <span class="+ topic/ph pr-d/codeph codeph"></span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定配置文件的位置。 如果未使用此选项，Media Packager将在工作目录中查找<span class="filepath"> flashaccessools.properties </span>。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <span class="+ topic/ph pr-d/codeph codeph">加密文件</span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">显示有关已打包的文件的信息。 源文件和目标文件不是必需的。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-dm <span class="+ topic/ph pr-d/codeph codeph"> metadatafile </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">显示有关现有元数据的信息。 源文件和目标文件不是必需的。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-e </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">将此选项与<span class="codeph"> -d </span>一起使用，从打包文件中提取策略。 将使用文件名和策略标识符在与加密文件相同的目录中创建文件。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-h </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">与<span class="codeph"> -d </span>一起使用，从打包的文件中提取DRM头。 使用文件名和扩展名<span class="filepath"> .header </span>在与加密文件相同的目录中创建文件 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-i <span class="+ topic/ph pr-d/codeph codeph"> contentID </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定此内容段的唯一标识符。 如果未指定标识符，则将使用目标文件名。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-k <span class="+ topic/ph pr-d/codeph codeph">键</span>= <span class="+ topic/ph pr-d/codeph codeph">值</span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定要添加到内容元数据的自定义键/值。 可以指定多个<span class="codeph"> -k </span>选项。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-m </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">将此选项与<span class="codeph"> -d </span>一起使用，从打包的文件中提取元数据。 将使用文件名和扩展名<span class="codeph"> .metadata </span>在与加密文件相同的目录中创建文件。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-noprompt </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">不要询问是否应覆盖目标文件。 如果目标文件已存在且未设置<span class="codeph"> -o </span>，则将返回一个错误。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-o </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果目标文件已存在，则在不进行提示的情况下覆盖它。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-p <span class="+ topic/ph pr-d/codeph codeph">文件名[domain-transport-cert] </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定包含策略的文件的名称。 如果策略要求向使用与属性文件中指定的传输证书不同的传输证书的服务器进行域注册，则还需要提供域传输证书。 </p> <p class="- topic/p ">可以指定多个<span class="codeph"> -p </span>选项，默认情况下，客户端将使用第一个选项。 在命令行上指定的值优先于在配置文件中指定的值。 </p> </td> 
  </tr> 
 </tbody> 
</table>

