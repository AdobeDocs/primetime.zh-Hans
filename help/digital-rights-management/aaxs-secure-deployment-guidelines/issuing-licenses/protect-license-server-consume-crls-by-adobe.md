---
seo-title: 冲减按Adobe发布的CRL
title: 冲减按Adobe发布的CRL
uuid: 43f65edb-0c96-46ab-b787-1b5f0b4b093e
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---


# 使用Adobe{#consume-crls-published-by-adobe}发布的CRL

SDK会定期下载由Adobe发布的CRL。 请勿阻止访问这些文件或阻止强制执行这些CRL。

SDK具有一个配置选项，用于在检索AdobeCRL时忽略错误。 此选项只能用于开发环境。 在生产环境中，许可证服务器必须能够从Adobe检索CRL。 无法获取有效CRL是错误。
