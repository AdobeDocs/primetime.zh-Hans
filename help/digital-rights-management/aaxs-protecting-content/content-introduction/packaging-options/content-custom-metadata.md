---
title: 自定义元数据
description: 自定义元数据
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---


# 自定义元数据{#custom-metadata}

**指定自定义键/值以添加到可由服务器应用程序解释的内容元数据。**

Adobe Access内容元数据格式允许在打包时包含自定义密钥/值对，这些对将由许可证服务器在许可证发放期间进行处理。 此元数据与策略不同，对于每条内容都可以是唯一的。

示例用例：在测试阶段，您在打包时包含自定义属性“Release:BETA”。 许可证服务器可以在测试期内向此内容提供许可证，但在测试期结束后，许可证服务器将不允许访问该内容。
