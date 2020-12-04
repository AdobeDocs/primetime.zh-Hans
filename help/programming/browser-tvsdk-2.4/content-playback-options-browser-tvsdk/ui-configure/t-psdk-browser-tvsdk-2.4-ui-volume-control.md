---
description: 可以为音量设置用户界面控件。
seo-description: 可以为音量设置用户界面控件。
seo-title: 提供音量控制
title: 提供音量控制
uuid: 5f2f69cc-3969-4ca2-8ab9-5713fdf5cdb8
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---


# 提供卷控件{#provide-volume-control}

可以为音量设置用户界面控件。

1. 请等待`MediaPlayer`实例处于此命令的有效状态。

   除RELEASED或ERROR之外的任何状态都有效。
1. 在`MediaPlayer`实例上设置音量属性以设置音频音量。

   ```js
   player.volume = ...
   ```

   卷的值表示请求的卷占最大卷的比例，其中0为静音，是最大卷。

