---
title: 在BEES服务器上配置SSL
description: 在BEES服务器上配置SSL
copied-description: true
exl-id: 6823a71c-3be6-4c07-a3e6-e16bd931deaf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---

# 在BEES服务器上配置SSL {#configure-ssl-on-your-bees-server}

1. 向提供此软件的Adobe联系人提供服务器SSL证书。

   证书将作为受信任证书添加到Primetime Cloud DRM信任存储区。
1. 启用SSL连接的客户端身份验证（在此版本中禁用）：
   1. 添加 `[!DNL clouddrm-transport.cer]` 和 `[!DNL AdobeFlashAccessIntermediateCA.cer]` 用于客户端身份验证的信任存储区的证书。
   1. 在SSL配置中启用客户端身份验证。
