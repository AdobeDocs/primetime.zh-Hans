---
title: 常见问题解答
description: 常见问题解答
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# 常见问题解答 {#faq}

* ECI更改的频率如何？
   * 无论何时发布新的AdobeDRM客户端，都将添加ECI设备记录。

* ECI文件有多大？
   * 每条设备记录的字节数通常少于1 KB。

* 如果服务器缺少ECI设备记录，会发生什么情况？
   * 该特定类客户端将无法针对本地个性化服务器进行个性化，并且错误将记录到日志文件中。

* 如果服务器的CRL过期，会发生什么情况？
   * 服务器将停止正常运行，并且错误将记录到日志文件中。
