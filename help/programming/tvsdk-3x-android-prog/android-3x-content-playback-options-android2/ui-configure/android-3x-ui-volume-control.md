---
description: 您可以设置用户界面控件来调整视频的音量。
title: 提供音量控制
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# 提供音量控制 {#provide-volume-control}

您可以设置用户界面控件来调整视频的音量。

1. 在音量控制接口元素的回调例程中，确保播放器处于此命令的有效状态。

   >[!TIP]
   >
   >除RELEASED之外的任何状态均有效。

1. 调用 `setVolume` 设置音频音量。

   例如：

   ```java
   void setVolume(int volume) throws MediaPlayerException;
   ```

   卷的值表示请求的卷，以最大卷的比例表示，其中 `0` 安静且 `1` 是最大卷。
