---
title: 常见问题解答
description: 常见问题解答
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---


# 常见问题解答{#faq}

* ECI更改发生的频率是多久？
   * 每当发布新的Adobe DRM客户端时，都会添加ECI设备记录。

* ECI文件有多大？
   * 它们通常不到1 KB/台设备记录。

* 如果服务器缺少ECI设备记录，会发生什么情况？
   * 该特定类别的客户端将无法针对本地个性化服务器进行个性化，错误将记录到日志文件中。

* 如果服务器的CRL过期，会发生什么情况？
   * 服务器将停止正常工作，错误将记录到日志文件。