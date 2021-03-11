---
description: 您可以设置用户界面控件来调整视频的音量。
title: 提供音量控制
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 2%

---


# 提供卷控件{#provide-volume-control}

您可以设置用户界面控件来调整视频的音量。

1. 在卷控制接口元素的回调例程中，确保播放器处于此命令的有效状态。

   >[!TIP]
   >
   >除“已释放”之外的任何状态都有效。

1. 调用`setVolume`设置音频音量。

   例如：

   ```java
   void setVolume(int volume) throws MediaPlayerException;
   ```

   卷的值表示请求的卷占最大卷的比例，其中`0`为静音，`1`为最大卷。