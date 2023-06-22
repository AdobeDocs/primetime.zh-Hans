---
title: 命令行用法
description: 命令行用法
copied-description: true
exl-id: 55b18fee-b7d8-4a5a-91a7-a08cd23e7866
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# 命令行用法 {#command-line-usage}

在使用Media Packager之前，请确保您满足要求中列出的要求，并且配置文件包含必需的信息(请参阅 *使用Adobe访问引用实施*.

媒体包管理器位于 [!DNL \Reference Implementation\Command Line tools] 目录。 要加密单个文件，请使用以下语法：

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
* `dest` 指定将写入加密内容的位置。 如果指定了目录，则将使用与源文件相同的文件名将加密文件保存在此文件夹中，但该目录不能是包含源文件的目录。

要使用同一密钥加密多个文件（用于支持多比特率），请使用以下语法：

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

* `sourcefiles` 是以空格分隔的一系列源条目，表示要加密的文件。
* `dest-directory` 指定将写入加密内容的位置。 加密文件将使用与源文件相同的文件名保存在此文件夹中，但目录不能是包含源文件的目录。

要查看有关加密文件的信息，请使用以下语法：

```
java -jar AdobePackager.jar -d  
<i class="+ topic ph hi-d="" i "="">
  encryptedfile [-e] [-m] 
</i class="+ topic>
```

* `encryptedfile` 是加密文件。

要查看有关元数据文件的信息，请使用以下语法：

```
java -jar AdobePackager.jar -dm <metadatafile> [-e]
```

* `metadatafile` 是 [!DNL .metadata] 包含DRM元数据的文件。

>[!NOTE]
>
>在打包过程中，Media Packager在默认情况下将不再生成.header文件。 要生成此文件，请使用 `-h` 选项。

下表包含上述语法中所示的命令行选项说明：

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_wgz_spy_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">命令行选项 </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">描述 </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-c <span class="+ topic/ph pr-d/codeph codeph"> 配置文件 </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定配置文件的位置。 如果未使用此选项，媒体打包程序将查找 <span class="filepath"> flashaccesstools.properties </span> 工作目录下。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-d <span class="+ topic/ph pr-d/codeph codeph"> encryptedfile </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">显示有关已打包的文件的信息。 源文件和目标文件不是必需的。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-dm <span class="+ topic/ph pr-d/codeph codeph"> 元数据文件 </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">显示有关现有元数据的信息。 源文件和目标文件不是必需的。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-e </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">将此选项与 <span class="codeph"> -d </span> 从打包的文件中提取策略。 将使用文件名和策略标识符在与加密文件相同的目录中创建一个文件。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-h </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">使用方式 <span class="codeph"> -d </span> 从封装文件中提取DRM标头。 使用文件名和扩展名在与加密文件相同的目录中创建一个文件 <span class="filepath"> .header </span> </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-i <span class="+ topic/ph pr-d/codeph codeph"> contentid </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">为此内容段指定唯一标识符。 如果未指定标识符，则将使用destfile文件名。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-k <span class="+ topic/ph pr-d/codeph codeph"> 键 </span>= <span class="+ topic/ph pr-d/codeph codeph"> 值 </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定要添加到内容元数据的自定义键/值。 多个 <span class="codeph"> -k </span> 可以指定选项。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-m </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">将此选项与 <span class="codeph"> -d </span> 以从打包的文件中提取元数据。 将使用文件名和扩展名在与加密文件相同的目录中创建一个文件 <span class="codeph"> .metadata </span>. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-noprompt </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">不要询问是否应覆盖目标文件。 如果目标文件已存在，并且 <span class="codeph"> -o </span> 未设置，将返回错误。 </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-o </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">如果目标文件已存在，则在不提示的情况下覆盖该文件。 </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">-p <span class="+ topic/ph pr-d/codeph codeph"> 文件名[domain-transport-cert] </span> </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">指定包含策略的文件名。 如果策略要求向使用与属性文件中指定的传输证书不同的传输证书的服务器进行域注册，则还需要提供域传输证书。 </p> <p class="- topic/p ">多个 <span class="codeph"> -p </span> 可指定选项，客户端将默认使用第一个选项。 命令行中指定的值优先于配置文件中指定的值。 </p> </td> 
  </tr> 
 </tbody> 
</table>
