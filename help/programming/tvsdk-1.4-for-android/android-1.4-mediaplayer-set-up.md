---
description: 适用于Android的MediaPlayer界面封装了媒体播放器的功能和行为。
seo-description: 适用于Android的MediaPlayer界面封装了媒体播放器的功能和行为。
seo-title: 设置MediaPlayer
title: 设置MediaPlayer
uuid: 492b4693-acdf-4213-98e5-d6f0f1ae086d
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 设置MediaPlayer {#set-up-the-mediaplayer}

适用于Android的MediaPlayer界面封装了媒体播放器的功能和行为。

TVSDK提供一个接口 `MediaPlayer` 的实现，即类 `DefaultMediaPlayer` 。 当您需要视频播放功能时，请实例化 `DefaultMediaPlayer`。

>[!TIP]
>
>仅与界 `DefaultMediaPlayer` 面公开的方法与实例交互 `MediaPlayer` 。

1. 使用公共工厂方法实例化MediaPlayer, `DefaultMediaPlayer.create` 传递Java Android应用程序上下文对象。

   ```java
   public static MediaPlayer create(Context context) 
   ```

1. 调 `MediaPlayer.getView` 用以获取对实例的引 `MediaPlayerView` 用。

   ```java
   MediaPlayerView getView() throws IllegalStateException; 
   ```

1. 将实 `MediaPlayerView` 例放在 `FrameLayout` 一个实例中，该实例将视频放在设备的屏幕上。

   ```java
   FrameLayout playerFrame = (FrameLayout) view.findViewById(R.id.playerFrame); 
   playerFrame.addView(mediaPlayer.getView()); 
   ```

该实 `MediaPlayer` 例现已可用，并且已正确配置以在设备屏幕上显示视频内容。
