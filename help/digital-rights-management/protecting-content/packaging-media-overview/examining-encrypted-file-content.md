---
title: 检查加密文件内容
description: 检查加密文件内容
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---

# 检查加密文件内容{#examining-encrypted-file-content}

您可以使用Java API检查加密媒体文件的内容。

检查加密文件内容：

1. 设置开发环境并包含所有JAR文件。 请参阅 *设置SDK* 用于您的项目。
1. 创建 `MediaEncrypter` 实例。
1. 将加密文件传递到 `MediaEncrypter.examineEncryptedContent` 方法，返回 `KeyMetaData` 对象。

1. Inspect中的信息 `KeyMetaData` 对象。

有关描述如何从加密文件中提取DRM元数据的示例代码，请参阅 `com.adobe.flashaccess.samples.mediapackager.ExamineContent` 在参考实施命令行工具中 [!DNL samples/] 目录。
