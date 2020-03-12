---
description: 您可以控制隐藏式字幕的可见性。 启用可见性后，将显示当前选定的轨道。 如果更改当前轨道，则可见性设置将保持不变。
seo-description: 您可以控制隐藏式字幕的可见性。 启用可见性后，将显示当前选定的轨道。 如果更改当前轨道，则可见性设置将保持不变。
seo-title: 控制隐藏式字幕可见性
title: 控制隐藏式字幕可见性
uuid: f142e60d-5581-4d1c-9d4d-a4a58ac1b67b
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1

---


# 控制隐藏式字幕可见性 {#control-closed-caption-visibility}

您可以控制隐藏式字幕的可见性。 启用可见性后，将显示当前选定的轨道。 如果更改当前轨道，则可见性设置将保持不变。

>[!TIP]
>
>如果在播放器进入搜索模式时显示隐藏式字幕文本，则在搜索完成后不再显示该文本。 相反，几秒钟后，TVSDK在结束搜索位置之后显示视频中的下一个隐藏字幕文本。
>
>隐藏式字幕的可见性值在中定义 `MediaPlayer.Visibility`。>
>
```java>
>enum Visibility {  
>       VISIBLE,  
>       INVISIBLE 
>}
>```>



1. 请等待 `MediaPlayer` 至少处于“PREPARED”状态。 有关详细信息，请参 [阅等待有效状态](../../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/ui-configure/android-3x-ui-state-prepared-wait-for.md)。

1. 要获取隐藏式字幕的当前可见性设置，请使用中的getter方 `MediaPlayer`法，该方法返回可见性值。

   ```java
   MediaPlayer.Visibility getCCVisibility() throws MediaPlayerException;
   ```

1. 要更改隐藏式字幕的可见性，请使用setter方法，将可见性值从传递 `MediaPlayer.Visibility`。

   例如：

   ```java
   mediaPlayer.setCCVisibility(MediaPlayer.Visibility visibility);
   ```
