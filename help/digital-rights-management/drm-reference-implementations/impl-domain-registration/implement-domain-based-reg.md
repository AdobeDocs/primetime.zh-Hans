---
title: 实现基于身份的域注册
description: 实现基于身份的域注册
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
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
