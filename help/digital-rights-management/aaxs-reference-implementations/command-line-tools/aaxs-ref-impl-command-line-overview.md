---
title: '用于打包内容和创建撤销列表的命令行工具 '
description: '用于打包内容和创建撤销列表的命令行工具 '
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---


# 用于打包内容和创建撤销列表的命令行工具{#command-line-tools-for-packaging-content-revocation-lists}

该参考实现包含以下命令行工具：

* 策略管理器：用于创建和管理策略的工具
* 策略更新列表管理器：用于创建和查看策略更新列表的工具
* 吊销列表管理器：用于创建和查看吊销列表的工具
* Media Packager:用于创建加密FLV和F4V文件的工具
* AIR Publisher ID
* UtilityLicense Generator
* License Embedder

## 要求{#requirements}

使用参考实现中可用的命令行工具的要求如下：

* 所有命令行工具都需要Java 1.5或更高版本。
* 由Adobe颁发的Packager和License Server凭据（证书和密码）。 您需要凭据来加密和签署视频文件、签署策略更新和吊销列表以及预生成许可证。

>[!NOTE]
>
>由于Java错误，在命令行（如文件名、策略名或说明）上使用的参数只能使用操作系统默认字符集中的字符。

## 配置文件{#configuration-file}

一些命令行工具需要一个配置文件，其中包含这些工具用于应用策略和加密文件的信息。

默认配置文件为[!DNL flashaccesstools.properties]。 它位于工作目录中；即，运行工具的目录（请参阅安装命令行工具）。 每个工具还包含一个选项(`-c`)，如果您不希望使用默认值，可通过该选项指向要使用的配置文件。

配置文件使用Java属性文件格式。 如果任意属性的值包含特殊字符，请记住以下限制：

* 使用附加反斜杠进行反斜杠转义。 例如，要指定[!DNL C:\credentials.pfx]文件，请将其指定为[!DNL C:\\credentials.pfx]或`C:/credentials.pfx`。 要在网络服务器上指定文件，请指定`\\\\server\\folder\\filename.pfx`。
* 配置文件只能包含拉丁文–1字符。 如果必须使用非拉丁文–1字符，请使用相应的Unicode转义序列（也可以使用Java附带的[!DNL native2ascii]工具）。

在运行工具之前，在配置文件中设置属性值。 对于某些命令行工具，可以通过命令行或配置文件设置某些选项的值。 在这些情况下，通过命令行设置的值优先于配置文件中的任何值。

## 安装命令行工具{#installing-the-command-line-tools}

您可以从DVD上的[!DNL \Reference Implementation\Command Line Tools]目录复制所需的文件，该目录包含默认的[!DNL flashaccesstools.properties]配置文件，而[!DNL libs]目录包含工具的JAR文件。

[!DNL samples]目录包含几个示例Java源文件，用于演示Adobe Access SDK API的用法。 要构建和运行示例，请使用[!DNL build-samples.xml] Ant脚本。