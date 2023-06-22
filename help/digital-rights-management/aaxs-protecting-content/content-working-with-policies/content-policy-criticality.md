---
title: 策略重要性
description: 策略重要性
copied-description: true
exl-id: 6c6971fe-0c0a-4998-917c-aebbf1c4a9df
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# 策略重要性{#policy-criticality}

如果在策略中使用新的使用规则，并且这些策略用在针对旧版许可证服务器（不了解新的使用规则）打包的内容中，则可以指定旧版许可证服务器的行为方式。 默认情况下，策略关键度为“true”，这意味着许可证服务器必须了解策略的所有部分，才能使用策略生成许可证。 如果将策略重要性设置为“false”，则旧版许可证服务器可能会忽略它不了解的部分策略，并且服务器生成的许可证将不包含新的使用规则。

使用SDK版本2.0.2及更高版本的Adobe访问服务器将遵循策略重要性设置。
