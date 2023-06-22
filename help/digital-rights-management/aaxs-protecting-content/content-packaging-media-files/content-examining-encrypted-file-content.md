---
title: 检查加密文件内容
description: 检查加密文件内容
copied-description: true
exl-id: a8a61d1c-c259-4346-9a71-6741f70697ae
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# 检查加密文件内容 {#examining-encrypted-file-content}

要使用Java API检查FLV或F4V文件的内容，请执行以下步骤：

1. 设置开发环境，并包含中提到的所有JAR文件 [设置开发环境](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) 在您的项目中。
1. 创建 `MediaEncrypter` 实例。
1. 将加密文件传递到 `MediaEncrypter.examineEncryptedContent` 方法，返回一个 `KeyMetaData` 对象。
1. Inspect中的信息 `KeyMetaData` 对象。

有关演示如何从加密文件提取DRM元数据的示例代码，请参阅 `com.adobe.flashaccess.samples.mediapackager.ExamineContent` 在参考实施命令行工具“samples”目录中。
