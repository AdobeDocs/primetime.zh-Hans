---
title: 生成随机数
description: 生成随机数
copied-description: true
exl-id: 9a816570-753e-4b05-a6ea-2d4b20ffa3d4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '49'
ht-degree: 0%

---

# 生成随机数{#generating-random-numbers}

Linux服务器上可以使用硬件随机数生成器来确保生成足够的熵。 如果计算机无法生成足够的熵，则在等待来自的数据时将阻止需要随机性源的Adobe访问操作 `/dev/random`.
