---
title: 关于命令行工具配置文件
description: 关于命令行工具配置文件
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---

# 关于命令行工具配置文件{#about-command-line-tools-configuration-files}

命令行工具查找 [!DNL flashaccesstools.properties] 运行工具的目录中。 但是，您可以使用 `-c` 选项。 [!DNL flashaccesstools.properties]. 您还可以使用 `-c` 以指定其他配置文件。

命令行工具配置文件使用 *Java属性文件* 格式，适用于以下规则：

* 使用额外的反斜杠转义反斜杠。

  例如，在Windows计算机上，指定 [!DNL C:\credentials.pfx] 文件，您需要输入它为 [!DNL C:\\credentials.pfx] 或 `C:/credentials.pfx`. 要在Windows网络服务器上指定文件，需要输入 `\\\\server\\folder\\filename.pfx`
* 仅包括 *Latin-1* 个字符。

  要使用非&#x200B;*Latin-1* 字符之间，您需要使用相应的Unicode转义序列。 您可以选择应用 [!DNL native2ascii] 工具（随Java提供）添加到配置文件条目。
