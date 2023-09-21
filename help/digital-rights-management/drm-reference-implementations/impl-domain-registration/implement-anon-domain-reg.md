---
title: 实施匿名域注册
description: 实施匿名域注册
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '37'
ht-degree: 0%

---

# 实施匿名域注册{#implement-anonymous-domain-registration}

1. 创建指定需要域注册的DRM策略。
1. 将域服务器URL指定为：

   ```
   https://[host:port]/flashaccess/domainserver/domainname/
   ```

1. 强制进行匿名身份验证。

   在您的 [!DNL .properties] 文件，设置：

   ```
   policy.domain.anonymous=true 
   ```
