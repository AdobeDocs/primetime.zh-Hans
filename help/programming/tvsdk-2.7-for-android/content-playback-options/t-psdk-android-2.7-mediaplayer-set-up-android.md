---
description: 实例化MediaPlayer并将其视图放入帧布局中。
seo-description: 实例化MediaPlayer并将其视图放入帧布局中。
seo-title: 设置MediaPlayer
title: 设置MediaPlayer
uuid: 49c3edb9-b6e2-49f8-b4aa-f230af7de6b0
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 设置MediaPlayer {#set-up-the-mediaplayer}

TVSDK提供了用于创建高级视频播放器应用程序（您的Primetime播放器）的工具，您可以将其与其他Primetime组件集成。 它还提供了许多功能，旨在最大限度地提高视频回放质量。

实例化MediaPlayer并将其视图放入帧布局中。

1. 实例 `MediaPlayer`化，将对象 `android.content.Context` 传递到构造函数：

   ```java
   MediaPlayer mediaPlayer = new MediaPlayer(context);
   ```

1. 提供框架布局( `android.widget.FrameLayout`)以容纳以下 `ViewGroup` 各项 `mediaPlayer`:

   ```java
   FrameLayout playerFrame = (FrameLayout) _viewGroup.findViewById(R.id.playerFrame);
   ```

   以下是要创建的代码片断 `_viewGroup`。

   ```
   @Override 
    public ViewGroup onCreateView(LayoutInflater inflater, ViewGroup container, 
      Bundle savedInstanceState) { 
     _viewGroup = (ViewGroup) inflater.inflate( 
       R.layout.fragment_player, container, false); 
     return _viewGroup; 
    }
   ```

1. 将视图放在 `mediaPlayer` 框架布局中：

   ```java
   playerFrame.addView(mediaPlayer.getView());
   ```

>实 `MediaPlayer` 例( `mediaPlayer`)现已可用，并正确配置为在设备屏幕上显示视频内容。