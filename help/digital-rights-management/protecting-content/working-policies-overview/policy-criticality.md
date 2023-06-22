---
title: DRM政策重要性
description: DRM政策重要性
copied-description: true
exl-id: b9f5a095-9ec4-4ad7-8b70-9abae72d2a86
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# DRM政策重要性{#drm-policy-criticality}

如果您计划在DRM策略中应用新的使用规则，并且如果计划在已打包用于旧版许可证服务器的内容中使用此DRM策略（因此不能正确解释新的使用规则），您可能需要指定旧版许可证服务器的行为方式。 默认情况下，DRM策略重要性设置为 `true`.

此设置指示许可证服务器必须先处理DRM策略的所有部分，然后才能生成使用指定DRM策略的许可证。 如果DRM策略重要性设置为 `false`，旧版许可证服务器可能会忽略DRM策略中无法正确解释的部分。 因此，服务器生成的任何许可证不包括任何新的使用规则。

支持SDK版本2.0.2或更高版本的Primetime DRM服务器接受DRM策略重要性设置。
