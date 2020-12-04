---
description: 'null'
seo-description: 'null'
seo-title: 关于命令行工具配置文件
title: 关于命令行工具配置文件
uuid: 8220921f-1fe9-439c-8134-dc16c2e3601b
translation-type: tm+mt
source-git-commit: 0143d98185b9a63ef978aba18e2f3c8728333155
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---


# 关于命令行工具配置文件{#about-command-line-tools-configuration-files}

命令行工具在运行工具的目录中查找[!DNL flashaccesstools.properties]。 但是，运行命令行工具时，可以使用`-c`选项为默认[!DNL flashaccesstools.properties]指定其他位置。 还可以使用`-c`指定其他配置文件。

命令行工具配置文件使用&#x200B;*Java属性文件*&#x200B;格式，适用以下规则：

* 使用附加反斜杠转义反斜杠。

   例如，在Windows计算机上，要指定[!DNL C:\credentials.pfx]文件，您需要将其输入为[!DNL C:\\credentials.pfx]或`C:/credentials.pfx`。 要在Windows网络服务器上指定文件，您需要输入`\\\\server\\folder\\filename.pfx`
* 仅包含&#x200B;*拉丁语-1*&#x200B;字符。

   要使用非&#x200B;*拉丁语-1*&#x200B;字符，您需要使用相应的Unicode转义序列。 您可以选择将[!DNL native2ascii]工具（随Java一起提供）应用到配置文件条目。
