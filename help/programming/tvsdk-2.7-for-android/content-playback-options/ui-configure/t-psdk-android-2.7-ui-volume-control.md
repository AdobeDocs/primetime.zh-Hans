---
description: 您可以设置用户界面控件来调整视频的音量。
title: 提供音量控制
exl-id: 0daa87e2-51aa-4459-9a67-135dc54d09c7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# 提供音量控制 {#provide-volume-control}

您可以设置用户界面控件来调整视频的音量。

1. 在音量控制接口元素的回调例程中，确保播放器处于此命令的有效状态。

   >[!TIP]
   >
   >除RELEASED以外的任何状态均有效。

1. 调用 `setVolume` 设置音频音量。

   例如：

   ```java
   void setVolume(int volume) throws MediaPlayerException;
   ```

   卷的值表示请求的卷，以最大卷的比例表示，其中 `0` 是静音的 `1` 是最大卷。
