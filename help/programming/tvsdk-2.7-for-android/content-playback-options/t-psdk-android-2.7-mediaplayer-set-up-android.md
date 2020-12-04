---
description: 实例化MediaPlayer并将其视图放入帧布局中。
seo-description: 实例化MediaPlayer并将其视图放入帧布局中。
seo-title: 设置MediaPlayer
title: 设置MediaPlayer
uuid: 49c3edb9-b6e2-49f8-b4aa-f230af7de6b0
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# 设置MediaPlayer {#set-up-the-mediaplayer}

TVSDK提供用于创建高级视频播放器应用程序（您的Primetime播放器）的工具，您可以将其与其他Primetime组件集成。 它还提供许多旨在最大化视频回放质量的功能。

实例化MediaPlayer并将其视图放入帧布局中。

1. 实例化`MediaPlayer`，将`android.content.Context`对象传递给构造函数：

   ```java
   MediaPlayer mediaPlayer = new MediaPlayer(context);
   ```

1. 提供帧布局(`android.widget.FrameLayout`)以保存`mediaPlayer`的`ViewGroup`:

   ```java
   FrameLayout playerFrame = (FrameLayout) _viewGroup.findViewById(R.id.playerFrame);
   ```

   以下是用于创建`_viewGroup`的代码片断。

   ```
   @Override 
    public ViewGroup onCreateView(LayoutInflater inflater, ViewGroup container, 
      Bundle savedInstanceState) { 
     _viewGroup = (ViewGroup) inflater.inflate( 
       R.layout.fragment_player, container, false); 
     return _viewGroup; 
    }
   ```

1. 将视图`mediaPlayer`放在框架布局中：

   ```java
   playerFrame.addView(mediaPlayer.getView());
   ```

>`MediaPlayer`实例(`mediaPlayer`)现已可用，并且已正确配置为在设备屏幕上显示视频内容。