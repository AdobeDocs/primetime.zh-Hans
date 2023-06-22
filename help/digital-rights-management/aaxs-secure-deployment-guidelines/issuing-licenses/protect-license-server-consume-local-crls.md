---
title: 使用本地生成的CRL
description: 使用本地生成的CRL
copied-description: true
exl-id: d96418d0-8fd3-4f6d-8480-191fe540080a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# 使用本地生成的CRL{#consume-locally-generated-crls}

要使用本地生成的证书吊销列表(CRL)和策略更新列表，请使用Adobe访问API来验证签名。 这些API验证列表是否未被篡改，以及它们是否由正确的许可证服务器签名。

* 调用 `RevocationList.verifySignature` 在将RevocationList提供给任何API之前检查签名。

   有关更多信息，请参阅 `RevocationListFactory` 在 *Adobe访问API参考*.

* 调用 `PolicyUpdateList.verifySignature`以在提供 `PolicyUpdateList` 到任何API。

   有关更多信息，请参阅 `PolicyUpdateList` 在 *Adobe访问API参考*.
