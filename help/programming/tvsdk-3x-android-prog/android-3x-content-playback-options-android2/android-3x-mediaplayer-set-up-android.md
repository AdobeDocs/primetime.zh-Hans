---
description: TVSDK提供用于创建高级视频播放器应用程序（您的Primetime播放器）的工具，这些应用程序可以与其他Primetime组件集成。 它还提供了多种功能，旨在最大限度地提高视频回放质量。
title: 设置媒体播放器
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---


# 设置媒体播放器{#set-up-the-media-player}

TVSDK提供用于创建高级视频播放器应用程序（您的Primetime播放器）的工具，这些应用程序可以与其他Primetime组件集成。 它还提供了多种功能，旨在最大限度地提高视频回放质量。

<!--<a id="section_1FE83A68DE624F20B52C0959851F5699"></a>-->

实例化`MediaPlayer`并将其视图放入帧布局中。

1. 实例化`MediaPlayer`，将`android.content.Context`对象传递给构造函数：

   ```java
   MediaPlayer mediaPlayer = new MediaPlayer(context);
   ```

1. 提供帧布局(`android.widget.FrameLayout`)以容纳`mediaPlayer`的`ViewGroup`:

   ```java
   FrameLayout playerFrame = (FrameLayout) _viewGroup.findViewById(R.id.playerFrame);
   ```

   >[!NOTE]
   >
   >下面是用于创建`_viewGroup`的代码片断。

   ```
   @Override 
    public ViewGroup onCreateView(LayoutInflater inflater, ViewGroup container, 
      Bundle savedInstanceState) { 
     _viewGroup = (ViewGroup) inflater.inflate( 
       R.layout.fragment_player, container, false); 
     return _viewGroup; 
    }
   ```

1. 将`mediaPlayer`视图放在框架布局中：

   ```java
   playerFrame.addView(mediaPlayer.getView());
   ```

   >[!NOTE]
   >
   >`MediaPlayer`实例(`mediaPlayer`)现已可用，并且已正确配置，可在设备屏幕上显示视频内容。