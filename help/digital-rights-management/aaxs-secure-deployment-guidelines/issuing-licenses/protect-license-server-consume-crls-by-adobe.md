---
title: 使用由Adobe发布的CRL
description: 使用由Adobe发布的CRL
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---


# 使用由Adobe{#consume-crls-published-by-adobe}发布的CRL

SDK会定期下载由Adobe发布的CRL。 请勿阻止访问这些文件或阻止强制执行这些CRL。

SDK具有一个配置选项，可在检索AdobeCRL时忽略错误。 此选项只能用于开发环境。 在生产环境中，许可证服务器必须能够从Adobe检索CRL。 无法获取有效的CRL是错误。
