---
description: 您可以设置用户界面控件来调整视频的音量。
seo-description: 您可以设置用户界面控件来调整视频的音量。
seo-title: 提供音量控制
title: 提供音量控制
uuid: c87fe656-0329-4c9c-b65b-43be48c77062
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 1%

---


# 提供卷控件{#provide-volume-control}

您可以设置用户界面控件来调整视频的音量。

1. 在卷控制接口元素的回调例程中，确保播放器处于此命令的有效状态。

   >[!TIP]
   >
   >除RELEASED之外的任何状态都有效。

1. 调用`setVolume`设置音频音量。

   例如：

   ```java
   void setVolume(int volume) throws MediaPlayerException;
   ```

   卷的值表示所请求的卷占最大卷的比例，其中`0`是静音，`1`是最大卷。