---
description: Android的MediaPlayer界面封装媒体播放器的功能和行为。
title: 设置MediaPlay
exl-id: 2698fe8d-0b73-4aad-9fee-55d034d8ca64
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# 设置MediaPlay {#set-up-the-mediaplayer}

Android的MediaPlayer界面封装媒体播放器的功能和行为。

TVSDK提供以下实施之一 `MediaPlayer` 界面， `DefaultMediaPlayer` 类。 当您需要视频播放功能时，实例化 `DefaultMediaPlayer`.

>[!TIP]
>
>与 `DefaultMediaPlayer` 仅使用由公开的方法的实例 `MediaPlayer` 界面。

1. 使用公共实例化MediaPlayer `DefaultMediaPlayer.create` factory方法，传递Java Android应用程序上下文对象。

   ```java
   public static MediaPlayer create(Context context) 
   ```

1. 调用 `MediaPlayer.getView` 以获取 `MediaPlayerView` 实例。

   ```java
   MediaPlayerView getView() throws IllegalStateException; 
   ```

1. 放置 `MediaPlayerView` 中的实例 `FrameLayout` 实例，用于将视频放置在设备的屏幕上。

   ```java
   FrameLayout playerFrame = (FrameLayout) view.findViewById(R.id.playerFrame); 
   playerFrame.addView(mediaPlayer.getView()); 
   ```

此 `MediaPlayer` 实例现已可用，并且已正确配置为在设备屏幕上显示视频内容。
