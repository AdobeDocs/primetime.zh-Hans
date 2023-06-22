---
title: 许可证缓存持续时间
description: 许可证缓存持续时间
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---


# 许可证缓存持续时间{#license-caching-duration}

许可证缓存持续时间指定可以在客户端的本地许可证存储区的磁盘上缓存许可证的时长，而无需从许可证服务器重新获取。 或者，您可以指定一个绝对日期和时间，之后将不再缓存许可证。

一旦缓存过期日期，许可证就不再有效，客户端必须向许可证服务器请求新的许可证。

示例用例：使用许可证缓存持续时间指定特定许可证的固定有效时间量，例如在租赁用例中。 您可以指定30天租赁（使用许可证缓存）以指示使用内容的总许可证持续时间。
