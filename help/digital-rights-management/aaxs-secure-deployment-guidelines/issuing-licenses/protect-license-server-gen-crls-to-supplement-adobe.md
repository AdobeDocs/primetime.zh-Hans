---
seo-title: 生成CRL以补充Adobe发布的CRL
title: 生成CRL以补充Adobe发布的CRL
uuid: 4e93f6d3-5a04-44e9-9e6b-e878798b68f5
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 生成CRL以补充Adobe发布的CRL{#generate-crls-to-supplement-those-published-by-adobe}

Adobe Access允许您创建CRL以补充Adobe发布的计算机CRL。 Adobe Access SDK会检查并强制执行Adobe CRL，但是，您可以通过创建撤销其他计算机凭据的CRL来禁止其他客户端计算机。 为此，您必须将CRL传递给Adobe Access SDK，然后，在颁发许可证时，SDK将检查Adobe CRL和您自己的CRL。

要了解有关生成CRL的更多信息，请参 `RevocationListFactory` 阅 *Adobe Access API参考*。
