---
seo-title: 在BEES服务器上配置SSL
title: 在BEES服务器上配置SSL
uuid: 041a106e-8b21-4018-815d-b7ea48c3de03
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---


# 在BEES服务器{#configure-ssl-on-your-bees-server}上配置SSL

1. 向提供此软件的Adobe联系人提供您的服务器SSL证书。

   该证书将作为受信任证书添加到Primetime Cloud DRM信任存储。
1. 要启用SSL连接的客户端身份验证（在此版本中禁用）:
   1. 将`[!DNL clouddrm-transport.cer]`和`[!DNL AdobeFlashAccessIntermediateCA.cer]`证书添加到用于客户端身份验证的信任存储中。
   1. 在SSL配置中启用客户端身份验证。
