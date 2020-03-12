---
seo-title: 自定义元数据
title: 自定义元数据
uuid: 99bdef62-32a9-4fd0-919c-5a2594e8d17e
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# 自定义元数据 {#custom-metadata}

使用它向可由服务器应用程序解释的内容元数据中添加自定义键／值对。

Primetime DRM内容的元数据格式使您能够在打包时包含自定义键／值对。 然后，许可证服务器在发行许可证期间可以处理此自定义元数据。 元数据与Primetime DRM策略不同，并且对于每个内容部分都是唯一的。

示例用例：在测试阶段，您可以在打包时包含自 `Release:BETA` 定义属性。 许可证服务器可以在测试期内向此内容发放许可证。 但是，在测试期到期后，许可证服务器将不允许访问内容。
