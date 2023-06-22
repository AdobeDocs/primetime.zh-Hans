---
title: 预生成许可证
description: 预生成许可证
copied-description: true
exl-id: d0bdd722-fd0e-4f34-87e7-28a564daf82b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 0%

---

# 预生成许可证{#pre-generating-licenses}

如果您预生成包含基于时间的使用规则的许可证，则强烈建议该许可证包含同步要求(请参阅 *使用Adobe访问SDK保护内容* 指南)，以便安全地执行许可证过期。 如果您在许可证中有任何基于时间的限制，则强烈建议在客户端和服务器之间实施“心跳”机制，因为心跳会将客户端时间与服务器时间同步。
