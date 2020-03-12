---
seo-title: 配置和运行命令行工具
title: 配置和运行命令行工具
uuid: b65f8621-54fa-4927-b2f4-d2fd60350fc1
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# 配置和运行命令行工具 {#configure-and-run-the-command-line-tools}

命令行工具具有关联的属性，您必须先在中为这些属性设 [!DNL flashaccesstools.properties] 置 *值* ，然后才能运行工具。 某些命令行工具还允许您从命令行指定属性值。 您从命令行指定的值优先于您从提供的值 [!DNL flashaccesstools.properties]。

您必须修改下面几节中的设 [!DNL flashaccesstools.properties] 置，以启用您要使用的相应命令行工具：

* **Media Packager属性** -(适用于 [!DNL AdobePackager.jar])

* **策略更新列表管理器和撤销列表管理器属性** -(对于 [!DNL AdobePolicyUpdateListManager.jar] 和 [!DNL AdobeRevocationListManager.jar])

* **策略管理器属性** -(对于 [!DNL AdobePolicyManager.jar])

* **License Generator Properties** -(for [!DNL AdobeLicenseGenerator.jar])