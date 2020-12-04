---
description: 您可以使用Adobe PrimetimeDRM创建补充由Adobe发布的计算机CRL的CRL。
seo-description: 您可以使用Adobe PrimetimeDRM创建补充由Adobe发布的计算机CRL的CRL。
seo-title: 生成CRL以补充由Adobe发布的CRL
title: 生成CRL以补充由Adobe发布的CRL
uuid: 0cc4254d-20a0-4e05-9c5b-0b84a5c833cb
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 0%

---


# 生成CRL以补充由Adobe{#generating-crls-to-supplement-those-published-by-adobe}发布的CRL

您可以使用Adobe PrimetimeDRM创建补充由Adobe发布的计算机CRL的CRL。

Primetime DRM SDK检查并执行AdobeCRL。 但是，您可以通过创建CRL来禁止其他客户端计算机，该CRL通过将CRL传递到Primetime DRM SDK来撤消其他计算机凭据。 发出许可证时，SDK将检查AdobeCRL和您的CRL。

要生成CRL，请参阅[RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html)。
