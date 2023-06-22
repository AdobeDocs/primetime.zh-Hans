---
description: 您可以控制隐藏式字幕的可见性。 当可见性打开时，将显示当前选定的轨道。 如果更改当前跟踪，可视性设置将保持不变。
title: 控制隐藏式字幕可见性
exl-id: d9428744-1700-4917-b334-d6e0446eaf37
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# 概述 {#control-closed-caption-visibility}

您可以控制隐藏式字幕的可见性。 当可见性打开时，将显示当前选定的轨道。 如果更改哪个轨道为当前轨道，可见性设置将保持不变。

>[!TIP]
>
>如果在播放器进入搜寻模式时显示隐藏式字幕文本，则搜寻完成后不再显示文本。 相反，几秒钟后，TVSDK会在视频中在结束搜寻位置后显示下一个隐藏式字幕文本。

>[!NOTE]
>
>隐藏式字幕的可见性值在中定义 `MediaPlayer.Visibility`.
>
>
```java
>enum Visibility { 
>       VISIBLE,  
>       INVISIBLE 
>}
>```

1. 等待MediaPlayer至少处于“已准备”状态(请参阅 [等待有效的状态](../../../tvsdk-1.4-for-android/ui-configure/android-1.4-ui-state-prepared-wait-for.md))。
1. 要获取隐藏式字幕的当前可见性设置，请使用MediaPlayer中的getter方法，该方法会返回可见性值。

   ```java
   Visibility getCCVisibility() throws IllegalStateException;
   ```

1. 要更改隐藏式字幕的可见性，请使用setter方法，从传递可见性值 `MediaPlayer.Visibility`.

   例如：

   ```java
   mediaPlayer.setCCVisibility(Visibility.VISIBLE);
   ```
