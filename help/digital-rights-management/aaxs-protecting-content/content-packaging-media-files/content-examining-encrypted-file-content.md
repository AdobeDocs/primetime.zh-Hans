---
seo-title: 检查加密的文件内容
title: 检查加密的文件内容
uuid: 2132fac7-5f11-4308-b511-ed4f216527a6
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# 检查加密的文件内容{#examining-encrypted-file-content}

要使用Java API检查FLV或F4V文件的内容，请执行以下步骤：

1. 设置开发环境并包含[设置项目中的开发环境](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md)中提及的所有JAR文件。
1. 创建`MediaEncrypter`实例。
1. 将加密文件传递给`MediaEncrypter.examineEncryptedContent`方法，该方法返回`KeyMetaData`对象。
1. Inspect`KeyMetaData`对象中的信息。

有关演示如何从加密文件提取DRM元数据的示例代码，请参见Reference Implementation Command Line Tools &quot;samples&quot;目录中的`com.adobe.flashaccess.samples.mediapackager.ExamineContent`。
