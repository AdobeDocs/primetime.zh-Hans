---
title: 预生成许可证
description: 预生成许可证
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '80'
ht-degree: 0%

---

# 预生成许可证{#pre-generating-licenses}

如果您预生成包含基于时间的使用规则的许可证，则强烈建议该许可证包含同步要求(请参阅 *使用Adobe访问SDK保护内容* 指南)，以便能够安全地执行许可证过期。 如果许可证中有任何基于时间的限制，则强烈建议在客户端和服务器之间实施“心跳”机制，因为心率将使客户端时间与服务器时间同步。
