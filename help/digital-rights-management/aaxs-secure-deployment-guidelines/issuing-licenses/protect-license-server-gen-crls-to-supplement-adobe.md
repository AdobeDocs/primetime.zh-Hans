---
seo-title: 生成CRL以补充由Adobe发布的CRL
title: 生成CRL以补充由Adobe发布的CRL
uuid: 4e93f6d3-5a04-44e9-9e6b-e878798b68f5
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# 生成CRL以补充由Adobe{#generate-crls-to-supplement-those-published-by-adobe}发布的CRL

Adobe访问允许您创建CRL以补充Adobe发布的计算机CRL。 Adobe访问SDK会检查并强制AdobeCRL，但是，您可以通过创建撤销其他计算机凭据的CRL来禁止其他客户端计算机。 为此，您必须将CRL传递给Adobe访问SDK，然后，在颁发许可证时，SDK将检查AdobeCRL和您自己的CRL。

要了解有关生成CRL的更多信息，请参阅&#x200B;*Adobe访问API参考*&#x200B;中的`RevocationListFactory`。
