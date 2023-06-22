---
title: 生成CRL以补充Adobe发布的这些CRL
description: 生成CRL以补充Adobe发布的这些CRL
copied-description: true
exl-id: 05dc2159-fa7f-4772-9f25-c89370b4981e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# 生成CRL以补充Adobe发布的规则{#generate-crls-to-supplement-those-published-by-adobe}

Adobe访问允许您创建CRL以补充Adobe发布的计算机CRL。 Adobe访问SDK会检查并强制执行AdobeCRL，但是，您可以通过创建可撤销其他计算机凭据的CRL来禁止其他客户端计算机。 为此，您必须将CRL传递给Adobe访问SDK，然后在颁发许可证时，SDK会检查AdobeCRL和您自己的CRL。

要了解有关生成CRL的更多信息，请参阅 `RevocationListFactory` 在 *Adobe访问API参考*.
