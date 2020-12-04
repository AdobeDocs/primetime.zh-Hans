---
description: SDK会定期下载由Adobe发布的CRL。 必须确保不阻止访问这些文件，或不阻止执行这些CRL。
seo-description: SDK会定期下载由Adobe发布的CRL。 必须确保不阻止访问这些文件，或不阻止执行这些CRL。
seo-title: 使用由Adobe发布的CRL
title: 使用由Adobe发布的CRL
uuid: 7a9088bd-dde6-4445-958c-3e7272215b3c
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---


# 使用Adobe{#consuming-crls-published-by-adobe}发布的CRL

SDK会定期下载由Adobe发布的CRL。 必须确保不阻止访问这些文件，或不阻止执行这些CRL。

SDK具有一个配置选项，用于在检索AdobeCRL时忽略错误，并且您只能在开发环境中应用此选项。 在生产环境中，许可证服务器必须从Adobe检索CRL。 如果许可证服务器无法获取有效的CRL，则出现错误。
