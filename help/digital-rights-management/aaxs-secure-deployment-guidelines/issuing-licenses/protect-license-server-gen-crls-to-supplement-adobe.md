---
title: 生成CRL以补充Adobe发布的那些规则
description: 生成CRL以补充Adobe发布的那些规则
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# 生成CRL以补充Adobe发布的那些规则{#generate-crls-to-supplement-those-published-by-adobe}

Adobe访问允许您创建CRL以补充由Adobe发布的计算机CRL。 Adobe访问SDK检查并强制执行AdobeCRL，但是，您可以通过创建可撤销其他计算机凭据的CRL来禁止其他客户端计算机。 为此，您必须将CRL传递给AdobeAccess SDK，然后在颁发许可证时，SDK会检查AdobeCRL和您自己的CRL。

要了解有关生成CRL的更多信息，请参阅 `RevocationListFactory` 在 *Adobe访问API参考*.
