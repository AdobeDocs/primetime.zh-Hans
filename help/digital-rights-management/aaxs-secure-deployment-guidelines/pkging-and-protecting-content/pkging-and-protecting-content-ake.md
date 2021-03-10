---
title: 非对称密钥加密
description: 非对称密钥加密
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---


# 非对称密钥加密{#asymmetric-key-encryption}

非对称密钥加密（也称为公钥加密）使用对密钥。 一个密钥用于加密；另一个是解密。 解密密钥被保密，并被称为&#x200B;*私钥*。 加密密钥（称为&#x200B;*公钥*）对任何已授权加密内容的人可用。 有权访问公钥的任何人都可以加密内容，但只有有权访问私钥的人才能解密内容。 无法从公钥重建私钥。

打包内容时，许可证服务器的公钥用于加密DRM元数据中的内容加密密钥(CEK)。 您必须确保只有许可证服务器才能访问许可证服务器的私钥；如果有人有密钥，他们可以解密和视图内容。

***注意：**请确保从受信任源处获得License Server的证书（包含公钥），以确保它是License Server的密钥，而不是无管理公钥。如果攻击者用其公钥替换许可证服务器的密钥，他们将能够解密您的内容。*

有关打包内容的详细信息，请参阅&#x200B;*使用Adobe Access SDK for Protecting Content*。
