---
title: 自定义元数据
description: 自定义元数据
copied-description: true
exl-id: d7783420-b345-44de-8f22-a16dda5d7554
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---

# 自定义元数据 {#custom-metadata}

**指定要添加到可由服务器应用程序解释的内容元数据的自定义键/值。**

Adobe访问内容元数据格式允许在打包时包含自定义键/值对，以便在许可证颁发期间由许可证服务器处理。 此元数据与策略不同，并且对于每段内容可以是唯一的。

示例用例：在Beta版阶段，您需要在打包时包含自定义属性“Release：BETA”。 许可证服务器可以在Beta版期间销售此内容的许可证，但在Beta版到期后，许可证服务器将禁止访问此内容。
