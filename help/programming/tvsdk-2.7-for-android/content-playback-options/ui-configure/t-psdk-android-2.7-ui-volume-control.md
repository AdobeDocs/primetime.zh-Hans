---
description: 您可以设置用户界面控件来调整视频的音量。
seo-description: 您可以设置用户界面控件来调整视频的音量。
seo-title: 提供音量控制
title: 提供音量控制
uuid: f1e959e0-1817-4ccb-8adc-3eba09c91887
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 提供音量控制 {#provide-volume-control}

您可以设置用户界面控件来调整视频的音量。

1. 在卷控制接口元素的回调例程中，确保播放器处于此命令的有效状态。

   >[!TIP]
   >
   >除“已发布”之外的任何状态均有效。

1. 调 `setVolume` 用以设置音频音量。

   例如：

   ```java
   void setVolume(int volume) throws MediaPlayerException;
   ```

   卷的值表示所请求的卷占最大卷的比例，其中 `0` 为silent, `1` 是最大卷。

