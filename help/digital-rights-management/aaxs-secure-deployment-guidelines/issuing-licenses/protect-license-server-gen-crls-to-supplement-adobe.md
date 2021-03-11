---
title: 生成CRL以补充由Adobe发布的CRL
description: 生成CRL以补充由Adobe发布的CRL
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# 生成CRL以补充由Adobe{#generate-crls-to-supplement-those-published-by-adobe}发布的CRL

Adobe访问允许您创建CRL以补充由Adobe发布的计算机CRL。 Adobe访问SDK会检查并强制使用AdobeCRL，但是，您可以通过创建撤销其他计算机凭据的CRL来禁止其他客户端计算机。 为此，您必须将CRL传递给Adobe Access SDK，然后，在颁发许可证时，SDK将检查AdobeCRL和您自己的CRL。

要了解有关生成CRL的详细信息，请参阅&#x200B;*Adobe访问API参考*&#x200B;中的`RevocationListFactory`。
