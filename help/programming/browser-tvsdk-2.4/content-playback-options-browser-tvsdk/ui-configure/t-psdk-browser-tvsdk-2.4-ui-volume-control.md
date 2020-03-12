---
description: 您可以为音量设置用户界面控件。
seo-description: 您可以为音量设置用户界面控件。
seo-title: 提供音量控制
title: 提供音量控制
uuid: 5f2f69cc-3969-4ca2-8ab9-5713fdf5cdb8
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 提供音量控制{#provide-volume-control}

您可以为音量设置用户界面控件。

1. 等待实 `MediaPlayer` 例处于此命令的有效状态。

   除“已发布”或“错误”之外的任何状态都有效。
1. 在实例上设置volume属 `MediaPlayer` 性以设置音频音量。

   ```js
   player.volume = ...
   ```

   卷的值表示所请求的卷占最大卷的比例，其中0是silent，是最大卷。

