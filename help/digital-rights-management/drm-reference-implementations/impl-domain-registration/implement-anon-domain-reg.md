---
title: 实施匿名域注册
description: 实施匿名域注册
copied-description: true
exl-id: 304cfe6f-0917-42ef-a49a-e6c4bc9c10d0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '37'
ht-degree: 0%

---

# 实施匿名域注册{#implement-anonymous-domain-registration}

1. 创建一个DRM策略，该策略指定域注册是必需的。
1. 将域服务器URL指定为：

   ```
   https://[host:port]/flashaccess/domainserver/domainname/
   ```

1. 强制进行匿名身份验证。

   在您的 [!DNL .properties] 文件，设置：

   ```
   policy.domain.anonymous=true 
   ```
