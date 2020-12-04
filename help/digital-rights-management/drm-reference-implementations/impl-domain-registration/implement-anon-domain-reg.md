---
seo-title: 实现匿名域注册
title: 实现匿名域注册
uuid: 330d32fd-8c23-40f9-949b-635e5a9acc86
translation-type: tm+mt
source-git-commit: 4102780d0c7d0b96d120c1c2b3d14c47bc1b0e6f
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

1. 强制使用匿名身份验证。

   在[!DNL .properties]文件中，设置：

   ```
   policy.domain.anonymous=true 
   ```
