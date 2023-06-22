---
description: 您可以控制隐藏式字幕的可见性。 启用可见性后，将显示当前选定的曲目。 如果更改哪个轨道为当前轨道，可见性设置将保持不变。
title: 控制隐藏式字幕可见性
exl-id: 1fe978c5-b9ae-4e72-ac32-e3ba4e948683
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# 控制隐藏式字幕可见性 {#control-closed-caption-visibility}

您可以控制隐藏式字幕的可见性。 启用可见性后，将显示当前选定的曲目。 如果更改哪个轨道为当前轨道，可见性设置将保持不变。

>[!TIP]
>
>如果在播放器进入搜寻模式时显示隐藏式字幕文本，则搜寻完成后不再显示文本。 相反，几秒钟后，TVSDK会在视频中在结束搜寻位置后显示下一个隐藏式字幕文本。
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

1. 等待 `MediaPlayer` 至少处于“已准备”状态。 有关更多信息，请参阅 [等待有效状态](../../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/ui-configure/android-3x-ui-state-prepared-wait-for.md).

1. 要获取隐藏式字幕的当前可见性设置，请在中使用getter方法 `MediaPlayer`，返回可见性值。

   ```java
   MediaPlayer.Visibility getCCVisibility() throws MediaPlayerException;
   ```

1. 要更改隐藏式字幕的可见性，请使用setter方法，从传递可见性值 `MediaPlayer.Visibility`.

   例如：

   ```java
   mediaPlayer.setCCVisibility(MediaPlayer.Visibility visibility);
   ```
