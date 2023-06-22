---
title: 自定义元数据
description: 自定义元数据
copied-description: true
exl-id: cfc8b17b-c077-4b28-896d-b1ede1d5090b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---

# 自定义元数据 {#custom-metadata}

使用此选项可将自定义键/值对添加到可由服务器应用程序解释的内容元数据。

Primetime DRM内容的元数据格式允许您在打包时包含自定义键/值对。 然后，许可证服务器可以在许可证颁发期间处理此自定义元数据。 元数据与Primetime DRM策略不同，并且对于内容的每个部分可以是唯一的。

示例用例：在测试阶段，您可以包含自定义属性 `Release:BETA` 在打包时。 许可证服务器可以在Beta版期间向此内容销售许可证。 但是，在Beta版过期后，许可证服务器将禁止访问该内容。
