---
description: 可以为音量设置用户界面控件。
seo-description: 可以为音量设置用户界面控件。
seo-title: 提供音量控制
title: 提供音量控制
uuid: 63e96424-54d0-4c16-bd94-2366722f752a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---


# 提供卷控件{#provide-volume-control}

可以为音量设置用户界面控件。

1. 请等待MediaPlayer实例处于此命令的有效状态，该命令除RELEASED或ERROR外。
1. 调用`MediaPlayer`实例上的`setVolume`以设置音频音量。

   ```java
   void setVolume(int volume) throws IllegalStateException;
   ```

   卷的值表示请求的卷占最大卷的比例，其中0为silent,100为最大卷。

