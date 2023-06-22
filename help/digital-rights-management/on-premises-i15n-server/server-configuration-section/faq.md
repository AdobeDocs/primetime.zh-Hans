---
title: 常见问题解答
description: 常见问题解答
copied-description: true
exl-id: 9058604e-dbab-4df5-89fd-1219c85c7643
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# 常见问题解答 {#faq}

* ECI更改发生的频率如何？
   * 每当发布新的AdobeDRM客户端时，就会添加ECI设备记录。

* ECI文件有多大？
   * 每条设备记录通常小于1 KB。

* 如果服务器缺少ECI设备记录，会发生什么情况？
   * 该特定类客户端将无法针对本地个性化服务器进行个性化，并且错误将记录到日志文件中。

* 如果服务器的CRL过期，会发生什么情况？
   * 服务器将停止正常运行，并将错误记录到日志文件中。
