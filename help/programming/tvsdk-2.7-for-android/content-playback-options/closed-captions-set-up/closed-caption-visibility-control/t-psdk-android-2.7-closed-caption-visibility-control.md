---
description: 您可以控制隐藏式字幕的可见性。 启用可见性后，将显示当前选定的轨道。 如果更改当前跟踪，可视性设置将保持不变。
title: 控制隐藏式字幕的可见性
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---

# 概述 {#control-closed-caption-visibility-overview}

您可以控制隐藏式字幕的可见性。 启用可见性后，将显示当前选定的轨道。 如果更改当前跟踪，可视性设置将保持不变。

>[!TIP]
>
>如果在播放器进入搜寻模式时显示隐藏式字幕文本，则搜寻完成后不再显示文本。 相反，几秒后，TVSDK会在视频中在结束搜寻位置后显示下一个隐藏式字幕文本。
>
>隐藏式字幕的可见性值在中定义 `MediaPlayer.Visibility`.
>
>```java
>enum Visibility {  
>       VISIBLE,  
>       INVISIBLE 
>}
>```
>

1. 等待 `MediaPlayer` 至少处于“已准备”状态。

   有关更多信息，请参阅ui-state-prepared-wait-for 。
1. 要获取隐藏式字幕的当前可见性设置，请使用中的getter方法 `MediaPlayer`，返回可见性值。

   ```java
   MediaPlayer.Visibility getCCVisibility() throws MediaPlayerException;
   ```

1. 要更改隐藏式字幕的可见性，请使用setter方法，从中传递可见性值 `MediaPlayer.Visibility`.

   例如：

   ```java
   mediaPlayer.setCCVisibility(MediaPlayer.Visibility visibility);
   ```
