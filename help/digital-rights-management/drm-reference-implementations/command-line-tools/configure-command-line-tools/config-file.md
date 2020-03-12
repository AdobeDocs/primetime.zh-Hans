---
description: 'null'
seo-description: 'null'
seo-title: 关于命令行工具配置文件
title: 关于命令行工具配置文件
uuid: 8220921f-1fe9-439c-8134-dc16c2e3601b
translation-type: tm+mt
source-git-commit: 0143d98185b9a63ef978aba18e2f3c8728333155

---


# 关于命令行工具配置文件{#about-command-line-tools-configuration-files}

命令行工具在运 [!DNL flashaccesstools.properties] 行工具的目录中查找。 但是，在运行命 `-c` 令行工具时，可以使用此选项为默认位置指定其他位置 [!DNL flashaccesstools.properties]。 您还可以使用 `-c` 指定其他配置文件。

命令行工具配置文件使用 *Java属性文件格式* ，适用以下规则：

* 使用其他反斜杠转义反斜杠。

   例如，在Windows计算机上，要指定文 [!DNL C:\credentials.pfx] 件，您需要将其输入为 [!DNL C:\\credentials.pfx] 或 `C:/credentials.pfx`。 要在Windows网络服务器上指定文件，您需要输入 `\\\\server\\folder\\filename.pfx`
* 仅包含 *拉丁语-1字符* 。

   要使用非拉丁&#x200B;*语1字符* ，您需要使用相应的Unicode转义序列。 您可以选择将该工 [!DNL native2ascii] 具（随Java一起提供）应用到配置文件条目。
