---
seo-title: 检查加密的文件内容
title: 检查加密的文件内容
uuid: 2132fac7-5f11-4308-b511-ed4f216527a6
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 检查加密的文件内容 {#examining-encrypted-file-content}

要使用Java API检查FLV或F4V文件的内容，请执行以下步骤：

1. 设置开发环境，并将“设置开发环境”中提 [及的所有JAR文件包含在项目中](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) 。
1. 创建实 `MediaEncrypter` 例。
1. 将加密的文件传递给 `MediaEncrypter.examineEncryptedContent` 返回对象的方 `KeyMetaData` 法。
1. 检查对象中的 `KeyMetaData` 信息。

有关演示如何从加密文件中提取DRM元数据的示例代码，请参 `com.adobe.flashaccess.samples.mediapackager.ExamineContent` 阅参考实施命令行工具“示例”目录。
