---
description: TVSDK提供用于创建高级视频播放器应用程序（您的Primetime播放器）的工具，您可以将其与其他Primetime组件集成。 它还提供许多旨在最大化视频回放质量的功能。
seo-description: TVSDK提供用于创建高级视频播放器应用程序（您的Primetime播放器）的工具，您可以将其与其他Primetime组件集成。 它还提供许多旨在最大化视频回放质量的功能。
seo-title: 设置媒体播放器
title: 设置媒体播放器
uuid: 1f672484-b340-4f92-8a47-dad4c9f3b3fc
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---


# 设置媒体播放器{#set-up-the-media-player}

TVSDK提供用于创建高级视频播放器应用程序（您的Primetime播放器）的工具，您可以将其与其他Primetime组件集成。 它还提供许多旨在最大化视频回放质量的功能。

<!--<a id="section_1FE83A68DE624F20B52C0959851F5699"></a>-->

实例化`MediaPlayer`并将其视图放入帧布局中。

1. 实例化`MediaPlayer`，将`android.content.Context`对象传递给构造函数：

   ```java
   MediaPlayer mediaPlayer = new MediaPlayer(context);
   ```

1. 提供帧布局(`android.widget.FrameLayout`)以保存`mediaPlayer`的`ViewGroup`:

   ```java
   FrameLayout playerFrame = (FrameLayout) _viewGroup.findViewById(R.id.playerFrame);
   ```

   >[!NOTE]
   >
   >以下是用于创建`_viewGroup`的代码片断。

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

   >[!NOTE]
   >
   >`MediaPlayer`实例(`mediaPlayer`)现已可用，并且已正确配置为在设备屏幕上显示视频内容。