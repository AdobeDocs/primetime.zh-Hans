---
description: 实例化MediaPlayer并将其视图放入框架布局中。
title: 设置MediaPlay
exl-id: e8fb6527-154b-4f7e-a128-525b5a3b3474
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# 设置MediaPlay {#set-up-the-mediaplayer}

TVSDK提供了用于创建高级视频播放器应用程序（您的Primetime播放器）的工具，您可以将其与其他Primetime组件集成。 它还提供了许多旨在最大化视频播放质量的功能。

实例化MediaPlayer并将其视图放入框架布局中。

1. 实例化 `MediaPlayer`，传递 `android.content.Context` 对象：

   ```java
   MediaPlayer mediaPlayer = new MediaPlayer(context);
   ```

1. 提供框架布局( `android.widget.FrameLayout`)，以保留 `ViewGroup` 之 `mediaPlayer`：

   ```java
   FrameLayout playerFrame = (FrameLayout) _viewGroup.findViewById(R.id.playerFrame);
   ```

   下面是要创建的代码片段 `_viewGroup`.

   ```
   @Override 
    public ViewGroup onCreateView(LayoutInflater inflater, ViewGroup container, 
      Bundle savedInstanceState) { 
     _viewGroup = (ViewGroup) inflater.inflate( 
       R.layout.fragment_player, container, false); 
     return _viewGroup; 
    }
   ```

1. 放置视图 `mediaPlayer` 在框架布局内：

   ```java
   playerFrame.addView(mediaPlayer.getView());
   ```

>此 `MediaPlayer` 实例( `mediaPlayer`)现已可用，并且已正确配置为在设备屏幕上显示视频内容。
