---
title: 检查加密的文件内容
description: 检查加密的文件内容
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---


# 正在检查加密的文件内容{#examining-encrypted-file-content}

您可以使用Java API检查加密媒体文件的内容。

要检查加密的文件内容，请执行以下操作：

1. 设置开发环境并包含所有JAR文件。 请参阅&#x200B;*为项目设置SDK*。
1. 创建`MediaEncrypter`实例。
1. 将加密文件传递给`MediaEncrypter.examineEncryptedContent`方法，该方法返回`KeyMetaData`对象。

1. Inspect `KeyMetaData`对象中的信息。

有关描述如何从加密文件提取DRM元数据的示例代码，请参阅Reference Implementation Command Line Tools [!DNL samples/]目录中的`com.adobe.flashaccess.samples.mediapackager.ExamineContent`。
