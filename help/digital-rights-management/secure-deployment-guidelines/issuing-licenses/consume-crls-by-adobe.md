---
description: SDK会定期下载由Adobe发布的CRL。 您必须确保不会阻止对这些文件的访问，或者不会阻止强制执行这些CRL。
title: 使用由Adobe发布的CRL
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# 使用由Adobe{#consuming-crls-published-by-adobe}发布的CRL

SDK会定期下载由Adobe发布的CRL。 您必须确保不会阻止对这些文件的访问，或者不会阻止强制执行这些CRL。

SDK具有一个配置选项，可在检索AdobeCRL时忽略错误，并且您只能在开发环境中应用此选项。 在生产环境中，许可证服务器必须从Adobe检索CRL。 如果许可证服务器无法获取有效的CRL，则发生错误。
