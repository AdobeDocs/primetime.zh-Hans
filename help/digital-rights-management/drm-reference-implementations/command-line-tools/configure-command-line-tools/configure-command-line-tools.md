---
title: 配置并运行命令行工具
description: 配置并运行命令行工具
copied-description: true
exl-id: ff0d4316-24e6-4a34-b332-abd737d6fcf9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---

# 配置并运行命令行工具 {#configure-and-run-the-command-line-tools}

命令行工具具有关联的属性，您必须为其设置值 [!DNL flashaccesstools.properties] *早于* 运行工具。 某些命令行工具还允许您从命令行指定属性值。 从命令行指定的值优先于提供的值 [!DNL flashaccesstools.properties].

您必须修改以下部分中的设置 [!DNL flashaccesstools.properties] 要启用要使用的相应命令行工具，请执行以下操作：

* **媒体打包程序属性** - (用于 [!DNL AdobePackager.jar])

* **策略更新列表管理器和吊销列表管理器属性** - (用于 [!DNL AdobePolicyUpdateListManager.jar] 和 [!DNL AdobeRevocationListManager.jar])

* **策略管理器属性** - (用于 [!DNL AdobePolicyManager.jar])

* **许可证生成器属性** - (用于 [!DNL AdobeLicenseGenerator.jar])
