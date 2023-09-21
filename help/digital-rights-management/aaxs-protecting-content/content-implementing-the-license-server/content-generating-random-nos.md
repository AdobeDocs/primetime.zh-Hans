---
title: 生成随机数
description: 生成随机数
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '49'
ht-degree: 0%

---

# 生成随机数{#generating-random-numbers}

在Linux服务器上可使用硬件随机数生成器以确保生成足够的熵。 如果计算机无法生成足够的熵，则在等待来自的数据时，将阻止需要随机性源的Adobe访问操作 `/dev/random`.
