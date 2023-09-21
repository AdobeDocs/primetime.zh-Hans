---
title: 请求证书
description: 请求证书
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# 请求证书{#requesting-certificates}

注册是向Adobe请求证书的过程。 您可以生成密钥并创建发送到Adobe的请求。 然后，Adobe会生成证书并将其发送给您。 Adobe不知道私钥的内容。 因此，如果任何硬件出现故障，则必须备份密钥以恢复密钥。

与License Server、Packager或Transport证书不同，Adobe不颁发域CA证书。 您可以从证书颁发机构获取此证书，也可以生成自签名证书。

有关如何获取Primetime DRM凭据的信息，请参阅* Primetime DRM证书注册指南*。
