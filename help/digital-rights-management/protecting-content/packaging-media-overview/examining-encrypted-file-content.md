---
seo-title: 检查加密的文件内容
title: 检查加密的文件内容
uuid: 1b3318f6-0850-43f2-9127-c72ea81a1bdf
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 检查加密的文件内容{#examining-encrypted-file-content}

您可以使用Java API检查加密媒体文件的内容。

要检查加密的文件内容，请执行以下操作：

1. 设置开发环境并包含所有JAR文件。 请参 *阅为项目设置SDK* 。
1. 创建实 `MediaEncrypter` 例。
1. 将加密的文件传递给 `MediaEncrypter.examineEncryptedContent` 返回对象的方 `KeyMetaData` 法。

1. 检查对象中的 `KeyMetaData` 信息。

有关描述如何从加密文件中提取DRM元数据的示例代码，请参 `com.adobe.flashaccess.samples.mediapackager.ExamineContent` 阅Reference Implementation Command Line Tools目录中的DRM [!DNL samples/] 元数据。
