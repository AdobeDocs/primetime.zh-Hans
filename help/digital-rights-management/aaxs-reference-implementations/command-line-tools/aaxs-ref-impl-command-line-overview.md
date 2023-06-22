---
title: 用于打包内容和创建撤销列表的命令行工具
description: 用于打包内容和创建撤销列表的命令行工具
copied-description: true
exl-id: 34305dab-a2f0-41c2-9a59-3261e8dea7e2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---

# 用于打包内容和创建撤销列表的命令行工具 {#command-line-tools-for-packaging-content-revocation-lists}

参考实施包括以下命令行工具：

* 策略管理器：用于创建和管理策略的工具
* 策略更新列表管理器：用于创建和查看策略更新列表的工具
* 撤消列表管理器：用于创建和查看撤消列表的工具
* Media Packager：用于创建加密的FLV和F4V文件的工具
* AIR发布者ID
* 实用工具许可证生成器
* 许可证嵌入程序

## 要求 {#requirements}

参考实施中提供的命令行工具的使用要求如下：

* 所有命令行工具都需要Java 1.5或更高版本。
* Adobe颁发的Packager和License Server凭据（证书和密码）。 您需要凭据来加密和签署视频文件、签署策略更新和吊销列表以及预生成许可证。

>[!NOTE]
>
>由于Java错误，在命令行中使用的参数（如文件名、策略名称或描述）只能使用操作系统默认字符集中的字符。

## 配置文件 {#configuration-file}

一些命令行工具需要一个配置文件，该文件包含用于应用策略和加密文件的工具的信息。

默认配置文件为 [!DNL flashaccesstools.properties]. 它位于工作目录中；即运行工具的目录（请参阅安装命令行工具）。 每个工具还包含一个选项( `-c`)，可让您指向希望使用的配置文件（如果您不想使用默认值）。

配置文件使用Java属性文件格式。 如果任何属性的值包含特殊字符，请记住以下限制：

* 使用其他反斜杠转义反斜杠。 例如，要指定 [!DNL C:\credentials.pfx] 文件，将其指定为 [!DNL C:\\credentials.pfx] 或 `C:/credentials.pfx`. 要在网络服务器上指定文件，请指定 `\\\\server\\folder\\filename.pfx`.
* 配置文件只能包含Latin-1字符。 如果必须使用非Latin-1字符，请使用相应的Unicode转义序列(使用（可选） [!DNL native2ascii] Java附带的工具)。

在运行工具之前，在配置文件中设置属性的值。 对于某些命令行工具，可以通过命令行或配置文件来设置某些选项的值。 在这些情况下，通过命令行设置的值优先于配置文件中的任何值。

## 安装命令行工具  {#installing-the-command-line-tools}

您可以从以下位置复制所需的文件 [!DNL \Reference Implementation\Command Line Tools] 目录，包含默认 [!DNL flashaccesstools.properties] 配置文件和 [!DNL libs] 目录，其中包含工具的JAR文件。

此 [!DNL samples] 目录包含多个示例Java源文件，用于演示如何使用Adobe访问SDK API。 要构建和运行示例，请使用 [!DNL build-samples.xml] 蚂蚁脚本。
