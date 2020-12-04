---
seo-title: DRM策略重要性
title: DRM策略重要性
uuid: ddc03142-7acb-4a9f-a367-e34cfc5e78ba
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---


# DRM策略重要性{#drm-policy-criticality}

如果您计划在DRM策略中应用新的使用规则，并且您计划在已打包用于旧版许可证服务器的内容（因此无法正确解释新的使用规则）中使用此DRM策略，则可能需要指定旧版许可证服务器的行为方式。 默认情况下，DRM策略重要性设置为`true`。

此设置表示许可证服务器必须处理DRM策略的所有部分，才能生成使用指定DRM策略的许可证。 如果DRM策略重要性设置为`false`，则旧版许可证服务器可能会忽略DRM策略中无法正确解释的部分。 因此，由服务器生成的任何许可证不包含任何新的使用规则。

支持SDK版本2.0.2或更高版本的Primetime DRM服务器接受DRM策略重要性设置。
