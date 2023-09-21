---
title: 自定义元数据
description: 自定义元数据
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---

# 自定义元数据 {#custom-metadata}

使用此选项可将自定义键/值对添加到可由服务器应用程序解释的内容元数据。

Primetime DRM内容的元数据格式允许您在打包时包含自定义键/值对。 然后，许可证服务器可以在许可证颁发期间处理此自定义元数据。 元数据与Primetime DRM策略不同，并且对于内容的每个部分都是唯一的。

示例用例：在测试阶段，您可以包含自定义属性 `Release:BETA` 在打包时。 许可证服务器可以在Beta版期间销售此内容的许可证。 但是，Beta版过期后，许可证服务器将禁止访问该内容。
