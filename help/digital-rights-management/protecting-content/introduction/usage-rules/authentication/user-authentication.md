---
title: 使用规则
description: 使用规则
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---

# 使用规则 {#usage-rules}

以下主题介绍可在Adobe Primetime DRM策略中指定的使用规则。

## 用户身份验证 {#user-authentication}

用户身份验证指定获取许可证是否需要凭据，例如用户名和密码。 如果指定了经过身份验证（基于身份）的许可，则服务器 ~~_身份验证_~~ 颁发许可证之前的用户。

示例用例：订阅服务在颁发内容许可证之前可能需要输入用户名和密码。 带有Digital Copy的DVD或蓝光光盘可提供代码或其他令牌作为付款证明，该代码或其他令牌可兑换为电子下载。
