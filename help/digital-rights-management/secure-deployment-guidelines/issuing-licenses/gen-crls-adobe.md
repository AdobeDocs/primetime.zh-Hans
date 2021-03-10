---
description: 可以使用Adobe Primetime DRM创建补充由Adobe发布的计算机CRL的CRL。
title: 生成CRL以补充由Adobe发布的CRL
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# 生成CRL以补充由Adobe{#generating-crls-to-supplement-those-published-by-adobe}发布的CRL

可以使用Adobe Primetime DRM创建补充由Adobe发布的计算机CRL的CRL。

Primetime DRM SDK检查并强制使用AdobeCRL。 但是，您可以通过创建CRL来禁止其他客户端计算机，该CRL通过将CRL传递到Primetime DRM SDK来撤消其他计算机凭据。 在您颁发许可证时，SDK会检查AdobeCRL和您的CRL。

要生成CRL，请参阅[RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html)。
