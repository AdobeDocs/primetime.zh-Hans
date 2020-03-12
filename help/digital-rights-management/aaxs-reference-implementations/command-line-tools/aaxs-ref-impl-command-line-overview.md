---
seo-title: '用于打包内容和创建撤销列表的命令行工具 '
title: '用于打包内容和创建撤销列表的命令行工具 '
uuid: 2c740521-2004-4320-88e1-118b84e80e31
translation-type: tm+mt
source-git-commit: a33e1f290fcf78e6f131910f6037f4803f7be98d

---


# 用于打包内容和创建撤销列表的命令行工具 {#command-line-tools-for-packaging-content-revocation-lists}

参考实现包括以下命令行工具：

* 策略经理：用于创建和管理策略的工具
* 策略更新列表管理器：用于创建和查看策略更新列表的工具
* 撤销列表管理器：用于创建和查看撤销列表的工具
* Media Packager:用于创建加密FLV和F4V文件的工具
* AIR Publisher ID
* UtilityLicense Generator
* License Embeder

## 要求 {#requirements}

使用参考实现中可用的命令行工具的要求如下：

* 所有命令行工具都需要Java 1.5或更高版本。
* 由Adobe颁发的Packager和License Server凭据（证书和密码）。 您需要凭据来加密和签署视频文件、签署“策略更新”和“撤销”列表以及预生成许可证。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>由于Java错误，命令行中使用的参数（如文件名、策略名或描述）只能使用操作系统默认字符集中的字符。

## 配置文件 {#configuration-file}

一些命令行工具需要一个配置文件，其中包含用于应用策略和加密文件的工具信息。

默认配置文件为 [!DNL flashaccesstools.properties]。 它位于工作目录中；即运行工具的目录（请参阅安装命令行工具）。 每个工具还包含一个选项( `-c`)，如果您不希望使用默认值，可通过它指向要使用的配置文件。

配置文件使用Java属性文件格式。 如果任意属性的值包含特殊字符，请记住以下限制：

* 使用其他反斜杠转义反斜杠。 例如，要指定文 [!DNL C:\credentials.pfx] 件，请将其指定为 [!DNL C:\\credentials.pfx] 或 `C:/credentials.pfx`。 要指定网络服务器上的文件，请指定 `\\\\server\\folder\\filename.pfx`。
* 配置文件只能包含拉丁语-1字符。 如果必须使用非拉丁语-1字符，请使用相应的Unicode转义序列(可选地，使用Java附带 [!DNL native2ascii] 的工具)。

在运行工具之前，在配置文件中设置属性的值。 对于某些命令行工具，可以通过命令行或配置文件为某些选项设置值。 在这些情况下，通过命令行设置的值优先于配置文件中的任何值。

## 安装命令行工具 {#installing-the-command-line-tools}

您可以从DVD上的目录（其中包含默认配置文件） [!DNL \Reference Implementation\Command Line Tools] 和目录(其中包含工具的JAR文 [!DNL flashaccesstools.properties] 件) [!DNL libs] 中复制所需的文件。

该目 [!DNL samples] 录包含几个演示Adobe Access SDK API使用情况的示例Java源文件。 要构建和运行示例，请使用 [!DNL build-samples.xml] Ant脚本。