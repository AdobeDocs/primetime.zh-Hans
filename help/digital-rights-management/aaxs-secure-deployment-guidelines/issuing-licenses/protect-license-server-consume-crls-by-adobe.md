---
title: 使用Adobe发布的CRL
description: 使用Adobe发布的CRL
copied-description: true
exl-id: b7f68a29-f834-4613-b64d-e610f660e6fc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---

# 使用Adobe发布的CRL{#consume-crls-published-by-adobe}

SDK定期下载Adobe发布的CRL。 请勿阻止对这些文件的访问或阻止实施这些CRL。

SDK提供了一个配置选项，用于在检索AdobeCRL时忽略错误。 此选项只能在开发环境中使用。 在生产环境中，许可证服务器必须能够从Adobe中检索CRL。 无法获取有效的CRL是一个错误。
