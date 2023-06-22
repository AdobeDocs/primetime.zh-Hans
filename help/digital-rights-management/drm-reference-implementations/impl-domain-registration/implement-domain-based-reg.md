---
title: 实施基于身份的域注册
description: 实施基于身份的域注册
copied-description: true
exl-id: e2f826a8-eea5-4d5f-ac4d-401d7a6c5373
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---

# 实施基于身份的域注册{#implement-identity-based-domain-registration}

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
