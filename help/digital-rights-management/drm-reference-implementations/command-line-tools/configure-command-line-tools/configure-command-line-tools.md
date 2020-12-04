---
seo-title: 配置和运行命令行工具
title: 配置和运行命令行工具
uuid: b65f8621-54fa-4927-b2f4-d2fd60350fc1
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---


# 配置并运行命令行工具{#configure-and-run-the-command-line-tools}

命令行工具具有关联的属性，您必须在运行工具的&#x200B;*之前在[!DNL flashaccesstools.properties]*&#x200B;中设置值。 一些命令行工具还允许您从命令行指定属性值。 您从命令行指定的值优先于从[!DNL flashaccesstools.properties]提供的值。

您必须修改[!DNL flashaccesstools.properties]下几节中的设置，以启用您要使用的相应命令行工具：

* **Media Packager属性** -(适用于 [!DNL AdobePackager.jar])

* **策略更新列表管理器和撤销列表管理器属性** -(对于 [!DNL AdobePolicyUpdateListManager.jar] 和 [!DNL AdobeRevocationListManager.jar])

* **策略管理器属性** -(适用于 [!DNL AdobePolicyManager.jar])

* **License Generator Properties**  -(for [!DNL AdobeLicenseGenerator.jar])