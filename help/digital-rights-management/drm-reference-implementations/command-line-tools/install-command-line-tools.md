---
title: 安装命令行工具
description: 安装命令行工具
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 0%

---


# 安装命令行工具{#install-the-command-line-tools}

1. 将[DRM SDK DVD]\Reference Implementation\Command Line Tools\目录的内容复制到您系统上的工作目录。

   [!DNL .../Command Line Tools/] 内容：

   * [!DNL flashaccesstools.properties]  — 命令行工具的默认配置文件。
   * [!DNL libs/]  — 包含命令行工具JAR文件
   * [!DNL samples/]  — 包含ant构建脚本() [!DNL build-samples.xml]和Java源文件。

      >[!NOTE]
      >
      >Java源文件演示如何使用Primetime DRM SDK API。 要构建并运行示例，请在[!DNL samples/]中运行[!DNL build-samples.xml] Ant脚本。