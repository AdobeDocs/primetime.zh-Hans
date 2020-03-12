---
description: 您可以为音量设置用户界面控件。
seo-description: 您可以为音量设置用户界面控件。
seo-title: 提供音量控制
title: 提供音量控制
uuid: 63e96424-54d0-4c16-bd94-2366722f752a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 提供音量控制{#provide-volume-control}

您可以为音量设置用户界面控件。

1. 等待MediaPlayer实例处于此命令的有效状态，该命令是除RELEASED或ERROR之外的任何命令。
1. 调用 `setVolume` 实例 `MediaPlayer` 以设置音频音量。

   ```java
   void setVolume(int volume) throws IllegalStateException;
   ```

   卷的值表示所请求的卷占最大卷的比例，其中0表示silent,100表示最大卷。

