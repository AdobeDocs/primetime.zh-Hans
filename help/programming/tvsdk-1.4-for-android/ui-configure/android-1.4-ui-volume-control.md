---
description: 您可以为音量设置用户界面控件。
title: 提供音量控制
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---

# 提供音量控制{#provide-volume-control}

您可以为音量设置用户界面控件。

1. 请等待MediaPlayer实例处于此命令的有效状态，该命令除RELEASED或ERROR外。
1. 调用 `setVolume` 在 `MediaPlayer` 用于设置音频音量的实例。

   ```java
   void setVolume(int volume) throws IllegalStateException;
   ```

   卷的值表示请求的卷，以最大卷的比例表示，其中0表示静音，100表示最大卷。
