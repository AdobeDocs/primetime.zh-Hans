---
description: 您可以使用Adobe Primetime DRM创建CRL，这些CRL是Adobe发布的计算机CRL的补充。
seo-description: 您可以使用Adobe Primetime DRM创建CRL，这些CRL是Adobe发布的计算机CRL的补充。
seo-title: 生成CRL以补充Adobe发布的CRL
title: 生成CRL以补充Adobe发布的CRL
uuid: 0cc4254d-20a0-4e05-9c5b-0b84a5c833cb
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# 生成CRL以补充Adobe发布的CRL{#generating-crls-to-supplement-those-published-by-adobe}

您可以使用Adobe Primetime DRM创建CRL，这些CRL是Adobe发布的计算机CRL的补充。

Primetime DRM SDK检查并执行Adobe CRL。 但是，您可以通过创建CRL来禁止其他客户端计算机，该CRL通过将CRL传递到Primetime DRM SDK来撤销其他计算机凭据。 在您发出许可证时，SDK会检查Adobe CRL和您的CRL。

要生成CRL，请参 [阅RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html)。
