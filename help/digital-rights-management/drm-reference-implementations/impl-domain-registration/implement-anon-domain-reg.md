---
title: 实现匿名域注册
description: 实现匿名域注册
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '37'
ht-degree: 0%

---


# 实现匿名域注册{#implement-anonymous-domain-registration}

1. 创建指定需要域注册的DRM策略。
1. 将域服务器URL指定为：

   ```
   https://[host:port]/flashaccess/domainserver/domainname/
   ```

1. 强制要求匿名身份验证。

   在[!DNL .properties]文件中，设置：

   ```
   policy.domain.anonymous=true 
   ```
