---
seo-title: 使用本地生成的CRL
title: 使用本地生成的CRL
uuid: 5a4519b8-6dbd-4921-9048-6c9f67aae18d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---


# 使用本地生成的CRL{#consume-locally-generated-crls}

要使用本地生成的证书撤销列表(CRL)和策略更新列表，请使用Adobe访问API验证签名。 这些API验证列表是否未被篡改，且它们是否已由正确的许可证服务器签名。

* 调用`RevocationList.verifySignature`检查签名，然后向任何API提供RevocationList。

   有关详细信息，请参阅&#x200B;*Adobe访问API参考*&#x200B;中的`RevocationListFactory`。

* 调用`PolicyUpdateList.verifySignature`检查签名，然后将`PolicyUpdateList`提供给任何API。

   有关详细信息，请参阅&#x200B;*Adobe访问API参考*&#x200B;中的`PolicyUpdateList`。

