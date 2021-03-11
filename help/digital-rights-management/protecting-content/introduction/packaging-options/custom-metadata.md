---
title: 自定义元数据
description: 自定义元数据
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---


# 自定义元数据{#custom-metadata}

使用它向可由服务器应用程序解释的内容元数据中添加自定义键/值对。

Primetime DRM内容的元数据格式使您能够在打包时包含自定义键/值对。 然后，许可证服务器在颁发许可证期间可以处理此自定义元数据。 元数据与Primetime DRM策略不同，对于每个内容部分都可以是唯一的。

示例用例：在测试阶段，可以在打包时包含自定义属性`Release:BETA`。 许可证服务器可以在测试期内向此内容提供许可证。 但是，在测试期到期后，许可证服务器将不允许访问内容。
