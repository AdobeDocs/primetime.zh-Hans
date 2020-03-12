---
seo-title: 安装命令行工具
title: 安装命令行工具
uuid: 42fe7d55-7b8e-4f44-8714-ddae6c086d6a
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# 安装命令行工具 {#install-the-command-line-tools}

1. 将 [DRM SDK DVD]\Reference Implementation\Command Line Tools\目录的内容复制到系统上的工作目录中。

   [!DNL .../Command Line Tools/] 内容：

   * [!DNL flashaccesstools.properties] -命令行工具的默认配置文件。
   * [!DNL libs/] -包含命令行工具JAR文件
   * [!DNL samples/] -包含ant构建脚本( [!DNL build-samples.xml])和Java源文件。

      >[!NOTE]
      >
      >Java源文件演示如何使用Primetime DRM SDK API。 要构建和运行示例，请在中运行 [!DNL build-samples.xml] Ant脚本 [!DNL samples/]。