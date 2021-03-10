---
title: 关于命令行工具配置文件
description: 关于命令行工具配置文件
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---


# 关于命令行工具配置文件{#about-command-line-tools-configuration-files}

命令行工具在运行工具的目录中查找[!DNL flashaccesstools.properties]。 但是，运行命令行工具时，可以使用`-c`选项为默认[!DNL flashaccesstools.properties]指定其他位置。 您还可以使用`-c`指定其他配置文件。

命令行工具配置文件使用&#x200B;*Java属性文件*&#x200B;格式，适用以下规则：

* 使用附加反斜杠进行反斜杠转义。

   例如，在Windows计算机上，要指定[!DNL C:\credentials.pfx]文件，您需要输入[!DNL C:\\credentials.pfx]或`C:/credentials.pfx`。 要在Windows网络服务器上指定文件，需要输入`\\\\server\\folder\\filename.pfx`
* 仅包含&#x200B;*拉丁语–1*&#x200B;字符。

   要使用非&#x200B;*Latin-1*&#x200B;字符，您需要使用相应的Unicode转义序列。 您可以选择将[!DNL native2ascii]工具（随Java一起提供）应用到配置文件条目。
