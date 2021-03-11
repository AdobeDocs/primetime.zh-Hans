---
description: 可以设置声音音量的用户界面控件。
title: 提供音量控制
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '87'
ht-degree: 0%

---


# 提供卷控件{#provide-volume-control}

可以设置声音音量的用户界面控件。

1. 等待`MediaPlayer`实例处于此命令的有效状态。

   除“已发布”或“错误”之外的任何状态都有效。
1. 在`MediaPlayer`实例上设置volume属性以设置音频音量。

   ```js
   player.volume = ...
   ```

   卷的值表示请求的卷占最大卷的比例，其中0为silent，是最大卷。

