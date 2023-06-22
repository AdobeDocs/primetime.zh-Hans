---
description: 您可以通过向相应的Expressplay令牌服务器发送令牌请求，为其加密内容生成Expressplay令牌。
title: Expressplay令牌
exl-id: 38faba06-6737-4dec-ac97-27db3124b993
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 0%

---

# Expressplay令牌 {#expressplay-tokens}

您可以通过向相应的Expressplay令牌服务器发送令牌请求，为其加密内容生成Expressplay令牌。

例如，以下URL：

```
https://wv-gen.service.expressplay.com/hms/wv/
token?customerAuthenticator=<your expressplay customer authenticator>
&kid=fd1a706ac2b36002888f6d4a414333c3
&contentKey=5438b719bf47a2f5678237477db2f9e6
&securityLevel=1
&hdcpOutputControl=0
```

为提供的内容加密密钥存储ID或CEKSID `kid` 参数和为提供的内容加密密钥或CEK `contentKey` 参数必须与用于打包的内容加密密钥存储ID和内容加密密钥匹配。 以下文本是令牌服务器响应的示例：

```
https://wv.service.expressplay.com/hms/wv/rights/
?ExpressPlayToken=AQAAABIDKbgAAABQbt68jktab0YRY-r9mo6VP
 VqDDvkHq78x4V9_AyBUTtcNFHw5JtNKlKrMt-4HBdJ3Fopr7fqFSBp
 SJ4o-d8teAkUZUtW3Od5V-SHsCLnAlbFW84K71h2xNUiMAvRcUFBG3bjxMQ
```

然后，您可以

* 使用返回的URL和查询作为许可证服务器URL，或者
* 从URL中取出查询，并将其作为HTTPPOST标头单独传递到ExpressPlayToken
