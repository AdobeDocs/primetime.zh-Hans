---
title: 使用本地生成的CRL
description: 使用本地生成的CRL
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---


# 使用本地生成的CRL{#consume-locally-generated-crls}

要使用本地生成的证书吊销列表(CRL)和策略更新列表，请使用Adobe访问API验证签名。 这些API验证列表是否未被篡改，以及它们是否已由正确的许可证服务器签名。

* 调用`RevocationList.verifySignature`检查签名，然后再将RevocationList提供给任何API。

   有关详细信息，请参阅&#x200B;*Adobe访问API参考*&#x200B;中的`RevocationListFactory`。

* 在将`PolicyUpdateList`提供给任何API之前，请调用`PolicyUpdateList.verifySignature`检查签名。

   有关详细信息，请参阅&#x200B;*Adobe访问API参考*&#x200B;中的`PolicyUpdateList`。

