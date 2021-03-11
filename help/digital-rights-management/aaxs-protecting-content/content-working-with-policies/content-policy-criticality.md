---
title: 策略关键性
description: 策略关键性
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# 策略重要性{#policy-criticality}

如果策略中使用了新的使用规则，并且这些策略用于为旧版许可证服务器打包的内容（这些内容不了解新的使用规则），则您可以指定旧版许可证服务器的行为方式。 默认情况下，策略重要性为“true”，这意味着许可证服务器必须了解策略的所有部分才能使用策略生成许可证。 如果策略重要性设置为“false”，则旧版许可证服务器可能会忽略其不理解的部分策略，并且服务器生成的许可证将不包含新的使用规则。

使用SDK版本2.0.2及更高版本的Adobe访问服务器将遵守策略重要性设置。
