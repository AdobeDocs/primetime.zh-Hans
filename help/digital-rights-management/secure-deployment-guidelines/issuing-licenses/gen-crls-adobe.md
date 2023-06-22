---
description: 您可以使用Adobe Primetime DRM创建CRL，以补充Adobe发布的计算机CRL。
title: 生成CRL以补充Adobe发布的CRL
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# 生成CRL以补充Adobe发布的CRL{#generating-crls-to-supplement-those-published-by-adobe}

您可以使用Adobe Primetime DRM创建CRL，以补充Adobe发布的计算机CRL。

Primetime DRM SDK会检查并强制执行AdobeCRL。 但是，您可以通过创建一个CRL来禁止其他客户端计算机，该CRL通过将CRL传递到Primetime DRM SDK来撤销其他计算机凭据。 当您颁发许可证时，SDK会检查AdobeCRL和您的CRL。

要生成CRL，请参阅 [RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html).
