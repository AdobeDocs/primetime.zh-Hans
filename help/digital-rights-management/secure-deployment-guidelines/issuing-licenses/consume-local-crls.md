---
description: 要使用本地生成的证书撤销列表(CRL)和策略更新列表，请使用Adobe Primetime DRM API验证签名。
seo-description: 要使用本地生成的证书撤销列表(CRL)和策略更新列表，请使用Adobe Primetime DRM API验证签名。
seo-title: 使用本地生成的CRL
title: 使用本地生成的CRL
uuid: 2e20b8ca-8606-4c27-b585-2f020b93be32
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# 使用本地生成的CRL {#consuming-locally-generated-crls}

要使用本地生成的证书撤销列表(CRL)和策略更新列表，请使用Adobe Primetime DRM API验证签名。

以下API验证列表是否未被篡改，以及列表是否已由正确的许可证服务器签名：

* 调用 [RevocationList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html#verifySignature(java.security.cert.X509Certificate)) ，以在向任何API提供 [RevocationList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html) 之前检查签名。

   有关详细信息，请参 [阅RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html)。

* 调用 [PolicyUpdateList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html#verifySignature(java.security.cert.X509Certificate)) ，以在向任何API提供签名之 `PolicyUpdateList` 前检查签名。

   有关详细信息，请参 [阅PolicyUpdateList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html)。

