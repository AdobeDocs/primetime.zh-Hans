---
seo-title: 使用本地生成的CRL
title: 使用本地生成的CRL
uuid: 5a4519b8-6dbd-4921-9048-6c9f67aae18d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 使用本地生成的CRL{#consume-locally-generated-crls}

要使用本地生成的证书撤销列表(CRL)和策略更新列表，请使用Adobe Access API验证签名。 这些API验证列表是否未被篡改，以及它们是否已经由正确的许可证服务器签名。

* 在向 `RevocationList.verifySignature` 任何API提供RevocationList之前，调用检查签名。

   有关详细信息，请参 `RevocationListFactory` 阅 *Adobe Access API参考*。

* 在 `PolicyUpdateList.verifySignature`向任何API提供签名之前，请调 `PolicyUpdateList` 用以检查签名。

   有关详细信息，请参 `PolicyUpdateList` 阅 *Adobe Access API参考*。

