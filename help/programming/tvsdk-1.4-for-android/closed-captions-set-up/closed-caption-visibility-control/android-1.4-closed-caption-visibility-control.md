---
description: 您可以控制隐藏式字幕的可见性。 当可见性打开时，将显示当前选定的轨道。 如果更改当前轨道，则可见性设置将保持不变。
seo-description: 您可以控制隐藏式字幕的可见性。 当可见性打开时，将显示当前选定的轨道。 如果更改当前轨道，则可见性设置将保持不变。
seo-title: 控制隐藏式字幕可见性
title: 控制隐藏式字幕可见性
uuid: 42913347-8158-474e-aa3c-ba4d38baba12
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# 概述{#control-closed-caption-visibility}

您可以控制隐藏式字幕的可见性。 当可见性打开时，将显示当前选定的轨道。 如果更改当前轨道，则可见性设置将保持不变。

>[!TIP]
>
>如果在播放器进入搜索模式时显示隐藏字幕文本，则在搜索完成后不再显示该文本。 相反，几秒钟后，TVSDK在结束搜索位置后显示视频中的下一个隐藏字幕文本。

>[!NOTE]
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

1. 请等待MediaPlayer至少拥有PREPARED状态（请参阅[等待有效状态](../../../tvsdk-1.4-for-android/ui-configure/android-1.4-ui-state-prepared-wait-for.md)）。
1. 要获取隐藏式字幕的当前可见性设置，请使用MediaPlayer中的getter方法，它返回一个可见性值。

   ```java
   Visibility getCCVisibility() throws IllegalStateException;
   ```

1. 要更改隐藏式字幕的可见性，请使用setter方法，将可见性值从`MediaPlayer.Visibility`传递。

   例如：

   ```java
   mediaPlayer.setCCVisibility(Visibility.VISIBLE);
   ```

