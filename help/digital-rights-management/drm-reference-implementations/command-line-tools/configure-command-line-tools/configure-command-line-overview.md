---
title: 概述
description: 概述
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---


# 概述{#overview}

命令行工具具有关联的属性，您必须为其设置值 [!DNL flashaccesstools.properties] *早于* 运行工具。 某些命令行工具还允许您从命令行指定属性值。 从命令行指定的值优先于提供的值 [!DNL flashaccesstools.properties].

您必须修改以下部分中的设置 [!DNL flashaccesstools.properties] 要启用要使用的相应命令行工具，请执行以下操作：

* **媒体打包程序属性** - (用于 [!DNL AdobePackager.jar])

* **策略更新列表管理器和吊销列表管理器属性** - (用于 [!DNL AdobePolicyUpdateListManager.jar] 和 [!DNL AdobeRevocationListManager.jar])

* **策略管理器属性** - (用于 [!DNL AdobePolicyManager.jar])

* **许可证生成器属性** - (用于 [!DNL AdobeLicenseGenerator.jar])

