---
title: 自定义元数据
description: 自定义元数据
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---

# 自定义元数据 {#custom-metadata}

**指定要添加到可由服务器应用程序解释的内容元数据的自定义键/值。**

Adobe访问内容元数据格式允许在打包时包含自定义密钥/值对，许可证服务器将在许可证颁发期间处理这些密钥/值对。 此元数据与策略是分开的，并且对于每段内容都可以是唯一的。

示例用例：在Beta测试阶段，您会在打包时包含自定义属性“Release：BETA”。 许可证服务器可以在Beta版期间销售此内容的许可证，但在Beta版到期后，许可证服务器将禁止访问此内容。
