---
description: 您可以为音量设置用户界面控件。
title: 提供音量控制
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '87'
ht-degree: 0%

---

# 提供音量控制{#provide-volume-control}

您可以为音量设置用户界面控件。

1. 等待 `MediaPlayer` 对于此命令处于有效状态的实例。

   除RELEASED或ERROR之外的任何状态均有效。
1. 在 `MediaPlayer` 用于设置音频音量的实例。

   ```js
   player.volume = ...
   ```

   卷的值表示请求的卷，以最大卷的比例表示，其中0表示静音，而最大卷表示最大卷。
