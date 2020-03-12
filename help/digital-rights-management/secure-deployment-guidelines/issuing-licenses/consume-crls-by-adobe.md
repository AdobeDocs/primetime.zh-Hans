---
description: SDK会定期下载Adobe发布的CRL。 您必须确保不会阻止对这些文件的访问，或者不会阻止执行这些CRL。
seo-description: SDK会定期下载Adobe发布的CRL。 您必须确保不会阻止对这些文件的访问，或者不会阻止执行这些CRL。
seo-title: 使用Adobe发布的CRL
title: 使用Adobe发布的CRL
uuid: 7a9088bd-dde6-4445-958c-3e7272215b3c
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 使用Adobe发布的CRL{#consuming-crls-published-by-adobe}

SDK会定期下载Adobe发布的CRL。 您必须确保不会阻止对这些文件的访问，或者不会阻止执行这些CRL。

SDK具有一个配置选项，可在检索Adobe CRL时忽略错误，并且您只能在开发环境中应用此选项。 在生产环境中，许可证服务器必须从Adobe检索CRL。 如果许可证服务器无法获得有效的CRL，则发生错误。
