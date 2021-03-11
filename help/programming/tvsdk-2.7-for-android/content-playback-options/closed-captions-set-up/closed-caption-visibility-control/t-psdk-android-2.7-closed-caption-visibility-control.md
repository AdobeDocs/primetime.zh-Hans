---
description: 您可以控制隐藏式字幕的可见性。 启用可见性后，将显示当前选定的轨道。 如果更改当前轨道，则可见性设置保持不变。
title: 控制隐藏字幕可见性
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 1%

---


# 概述{#control-closed-caption-visibility-overview}

您可以控制隐藏式字幕的可见性。 启用可见性后，将显示当前选定的轨道。 如果更改当前轨道，则可见性设置保持不变。

>[!TIP]
>
>如果当播放器进入搜索模式时显示隐藏字幕文本，则在搜索完成后不再显示该文本。 相反，几秒钟后，TVSDK在结束搜索位置后在视频中显示下一个隐藏字幕文本。
>
>隐藏式字幕的可见性值在`MediaPlayer.Visibility`中定义。
>
>
```java
>enum Visibility {  
>       VISIBLE,  
>       INVISIBLE 
>}
>```

1. 等待`MediaPlayer`至少处于PREPARED状态。

   有关详细信息，请参阅ui-state-prepared-wait-for。
1. 要获取隐藏字幕的当前可见性设置，请使用`MediaPlayer`中的getter方法，它返回一个可见性值。

   ```java
   MediaPlayer.Visibility getCCVisibility() throws MediaPlayerException;
   ```

1. 要更改隐藏式字幕的可见性，请使用setter方法，将可见性值从`MediaPlayer.Visibility`传递。

   例如：

   ```java
   mediaPlayer.setCCVisibility(MediaPlayer.Visibility visibility);
   ```

