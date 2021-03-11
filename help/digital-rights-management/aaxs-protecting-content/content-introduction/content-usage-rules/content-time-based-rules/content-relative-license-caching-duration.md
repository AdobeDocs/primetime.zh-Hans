---
title: 许可证缓存时间
description: 许可证缓存时间
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# 许可证缓存持续时间{#license-caching-duration}

指定许可证可以缓存在客户端本地许可证存储中磁盘上而无需从许可证服务器重新获取的持续时间。 您也可以指定一个绝对日期/时间，在此日期/时间之后，许可证将无法再缓存。

缓存过期日期过后，该许可证将不再有效，并且客户端必须从许可证服务器请求新的许可证。

示例用例：使用许可证缓存持续时间指定特定许可证的固定有效时间，例如在租赁用例中。 可以指定30天租赁（使用许可证缓存）以指示使用内容的总许可证持续时间。
