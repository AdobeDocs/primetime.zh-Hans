---
seo-title: 许可证缓存持续时间
title: 许可证缓存持续时间
uuid: 378940a2-f072-478d-bee1-05ccba888b5c
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# 许可证缓存持续时间{#license-caching-duration}

指定许可证可在客户端本地许可证存储中的磁盘上缓存的持续时间，无需从许可证服务器重新获取许可证。 您也可以指定一个绝对日期／时间，在该日期／时间之后，许可证将不能再缓存。

缓存到期日期过后，许可证不再有效，并且客户端必须从许可证服务器请求新许可证。

示例用例：使用许可证缓存持续时间来指定特定许可证的有效固定时间量，例如在租赁用例中。 可以指定30天租赁（带有许可证缓存）以指示使用内容的许可证总持续时间。
