---
description: 您可以为音量设置用户界面控件。
title: 提供音量控制
exl-id: 5c446081-5491-46b6-9259-293131af80cb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '87'
ht-degree: 0%

---

# 提供音量控制{#provide-volume-control}

您可以为音量设置用户界面控件。

1. 等待 `MediaPlayer` 对于此命令处于有效状态的实例。

   除RELEASED或ERROR之外的任何状态都有效。
1. 在上设置卷属性 `MediaPlayer` 实例来设置音频音量。

   ```js
   player.volume = ...
   ```

   卷的值表示请求的卷，以最大卷的比例表示，其中0表示静默，而最大卷表示最大卷。
