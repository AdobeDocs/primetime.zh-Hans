---
title: 配置和运行命令行工具
description: 配置和运行命令行工具
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---


# 配置并运行命令行工具{#configure-and-run-the-command-line-tools}

命令行工具具有关联的属性，您必须在[!DNL flashaccesstools.properties] *中设置值，然后才能运行工具*。 某些命令行工具还允许您从命令行指定属性值。 从命令行指定的值优先于从[!DNL flashaccesstools.properties]提供的值。

您必须修改[!DNL flashaccesstools.properties]下几节中的设置，以启用您要使用的相应命令行工具：

* **Media Packager属性** -(适 [!DNL AdobePackager.jar]用)

* **策略更新列表管理器和吊销列表管理器属性** -(对于 [!DNL AdobePolicyUpdateListManager.jar] 和 [!DNL AdobeRevocationListManager.jar])

* **策略管理器属性** -(适用于 [!DNL AdobePolicyManager.jar])

* **License Generator Properties** -(for  [!DNL AdobeLicenseGenerator.jar])