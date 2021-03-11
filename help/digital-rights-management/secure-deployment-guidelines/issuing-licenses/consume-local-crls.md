---
description: 要使用本地生成的证书吊销列表(CRL)和策略更新列表，请使用Adobe Primetime DRM API验证签名。
title: 使用本地生成的CRL
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---


# 正在使用本地生成的CRL {#consuming-locally-generated-crls}

要使用本地生成的证书吊销列表(CRL)和策略更新列表，请使用Adobe Primetime DRM API验证签名。

以下API验证列表未被篡改，且列表已由正确的许可证服务器签名：

* 在向任何API提供[ RevocationList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html)之前，请调用[RevocationList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationList.html#verifySignature(java.security.cert.X509Certificate))检查签名。

   有关详细信息，请参阅[RevocationListFactory](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/revocation/RevocationListFactory.html)。

* 调用[PolicyUpdateList.verifySignature](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html#verifySignature(java.security.cert.X509Certificate))检查签名，然后将`PolicyUpdateList`提供给任何API。

   有关详细信息，请参阅[PolicyUpdateList](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/policyupdate/PolicyUpdateList.html)。

