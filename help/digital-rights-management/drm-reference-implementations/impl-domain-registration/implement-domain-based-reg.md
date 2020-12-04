---
seo-title: 实现基于身份的域注册
title: 实现基于身份的域注册
uuid: 4a71b2e0-d1a2-4d63-9cbd-980a292774ab
translation-type: tm+mt
source-git-commit: 4102780d0c7d0b96d120c1c2b3d14c47bc1b0e6f
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---


# 实现基于身份的域注册{#implement-identity-based-domain-registration}

1. 创建具有强制域注册的DRM策略。
1. 指定域服务器URL的服务器主机和端口。

   在[!DNL .properties]文件中，设置：

   ```
   policy.domain.url=https://[server:port] 
   ```

1. 强制使用用户名和密码进行身份验证。

   在[!DNL .properties]文件中，设置：

   ```
   policy.domain.anonymous=false 
   ```
