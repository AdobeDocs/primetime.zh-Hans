---
description: 可以设置声音音量的用户界面控件。
title: 提供音量控制
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 0%

---


# 提供卷控件{#provide-volume-control}

可以设置声音音量的用户界面控件。

1. 等待MediaPlayer实例处于此命令的有效状态，该命令除RELEASED或ERROR外。
1. 调用`MediaPlayer`实例上的`setVolume`以设置音频音量。

   ```java
   void setVolume(int volume) throws IllegalStateException;
   ```

   卷的值表示请求的卷占最大卷的比例，其中0为silent，100为最大卷。

