---
description: 您可以通过向相应的Expressplay令牌服务器发送令牌请求，为加密内容生成Expressplay令牌。
seo-description: 您可以通过向相应的Expressplay令牌服务器发送令牌请求，为加密内容生成Expressplay令牌。
seo-title: Expressplay令牌
title: Expressplay令牌
uuid: 6103e1b2-127d-4758-a589-15f0f3c73db1
translation-type: tm+mt
source-git-commit: d0ba1f98b16f6350ae842ca2ce1261bf49dd8a66

---


# Expressplay令牌 {#expressplay-tokens}

您可以通过向相应的Expressplay令牌服务器发送令牌请求，为加密内容生成Expressplay令牌。

例如以下URL:

```
https://wv-gen.service.expressplay.com/hms/wv/
token?customerAuthenticator=<your expressplay customer authenticator>
&kid=fd1a706ac2b36002888f6d4a414333c3
&contentKey=5438b719bf47a2f5678237477db2f9e6
&securityLevel=1
&hdcpOutputControl=0
```

为参数提供的内容加密密钥存储ID或CEKSID以及为参数提供的内容加密密钥或CEK必须与用于打包的内容加密密钥存储ID和内容加密密钥相匹配。 `kid``contentKey` 以下文本是令牌服务器响应的示例：

```
https://wv.service.expressplay.com/hms/wv/rights/
?ExpressPlayToken=AQAAABIDKbgAAABQbt68jktab0YRY-r9mo6VP
 VqDDvkHq78x4V9_AyBUTtcNFHw5JtNKlKrMt-4HBdJ3Fopr7fqFSBp
 SJ4o-d8teAkUZUtW3Od5V-SHsCLnAlbFW84K71h2xNUiMAvRcUFBG3bjxMQ
```

然后，您可以

* 使用返回的URL和查询作为许可证服务器URL，或
* 从URL中取出查询，并作为HTTP POST头单独传入ExpressPlayToken