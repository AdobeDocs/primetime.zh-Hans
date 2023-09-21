---
title: 请求证书
description: 请求证书
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# 请求证书{#requesting-certificates}

注册是向Adobe请求证书的过程。 您可以生成密钥并创建发送到Adobe的请求。 然后，Adobe会生成证书并将其发送回您。 Adobe将不会知道私钥的内容。 因此，您必须有办法备份密钥，以便在发生硬件故障时可以恢复密钥。

与License Server、Packager或Transport证书不同，域CA证书不是由Adobe颁发的。 您可以从证书颁发机构获取此证书，也可以生成自签名证书。

有关如何获取Adobe访问凭据的说明，请参阅 *Adobe访问证书注册指南*.
