---
description: SDK定期下载Adobe发布的CRL。 您必须确保不阻止对这些文件的访问，或者不阻止实施这些CRL。
title: 使用Adobe发布的CRL
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# 使用Adobe发布的CRL{#consuming-crls-published-by-adobe}

SDK定期下载Adobe发布的CRL。 您必须确保不阻止对这些文件的访问，或者不阻止实施这些CRL。

SDK提供了一个配置选项，用于在检索AdobeCRL时忽略错误，并且您只能在开发环境中应用此选项。 在生产环境中，许可证服务器必须从Adobe中检索CRL。 如果许可证服务器无法获取有效的CRL，则出现错误。
