---
title: 实施基于标识的域注册
description: 实施基于标识的域注册
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---

# 实施基于标识的域注册{#implement-identity-based-domain-registration}

1. 创建具有强制域注册的DRM策略。
1. 为域服务器URL指定服务器的主机和端口。

   在您的 [!DNL .properties] 文件，设置：

   ```
   policy.domain.url=https://[server:port] 
   ```

1. 强制使用用户名和密码进行身份验证。

   在您的 [!DNL .properties] 文件，设置：

   ```
   policy.domain.anonymous=false 
   ```
