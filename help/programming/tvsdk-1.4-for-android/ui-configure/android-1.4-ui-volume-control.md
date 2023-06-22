---
description: 您可以为音量设置用户界面控件。
title: 提供音量控制
exl-id: aa8ffdf3-515b-4899-8a00-8fb5b8c595a9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---

# 提供音量控制{#provide-volume-control}

您可以为音量设置用户界面控件。

1. 请等待MediaPlayer实例处于此命令的有效状态，该命令除RELEASED或ERROR之外均有效。
1. 调用 `setVolume` 在 `MediaPlayer` 实例来设置音频音量。

   ```java
   void setVolume(int volume) throws IllegalStateException;
   ```

   卷的值表示所请求的卷，以最大卷的比例表示，其中0表示静音，100表示最大卷。
