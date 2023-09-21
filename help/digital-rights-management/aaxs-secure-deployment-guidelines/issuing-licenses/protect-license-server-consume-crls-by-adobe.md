---
title: 使用由Adobe发布的CRL
description: 使用由Adobe发布的CRL
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---

# 使用由Adobe发布的CRL{#consume-crls-published-by-adobe}

SDK定期下载Adobe发布的CRL。 请勿阻止对这些文件的访问或阻止强制实施这些CRL。

SDK具有配置选项，可在检索AdobeCRL时忽略错误。 此选项只能在开发环境中使用。 在生产环境中，许可证服务器必须能够从Adobe中检索CRL。 未能获取有效的CRL是一个错误。
