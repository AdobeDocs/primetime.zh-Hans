---
title: 生成随机数
description: 生成随机数
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '49'
ht-degree: 0%

---


# 生成随机数{#generating-random-numbers}

硬件随机数生成器可用于Linux服务器，以确保生成足够的熵。 如果计算机无法生成足够的熵，则需要随机性源的Adobe访问操作将在等待`/dev/random`中的数据时阻塞。
