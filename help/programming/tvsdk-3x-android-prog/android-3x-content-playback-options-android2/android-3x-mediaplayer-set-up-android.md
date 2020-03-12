---
description: TVSDK提供了用于创建高级视频播放器应用程序（您的Primetime播放器）的工具，您可以将其与其他Primetime组件集成。 它还提供了许多功能，旨在最大限度地提高视频回放质量。
seo-description: TVSDK提供了用于创建高级视频播放器应用程序（您的Primetime播放器）的工具，您可以将其与其他Primetime组件集成。 它还提供了许多功能，旨在最大限度地提高视频回放质量。
seo-title: 设置媒体播放器
title: 设置媒体播放器
uuid: 1f672484-b340-4f92-8a47-dad4c9f3b3fc
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 设置媒体播放器 {#set-up-the-media-player}

TVSDK提供了用于创建高级视频播放器应用程序（您的Primetime播放器）的工具，您可以将其与其他Primetime组件集成。 它还提供了许多功能，旨在最大限度地提高视频回放质量。

<!--<a id="section_1FE83A68DE624F20B52C0959851F5699"></a>-->

实例化 `MediaPlayer` 一个视图并将其放入框架布局中。

1. 实例 `MediaPlayer`化，将对象 `android.content.Context` 传递到构造函数：

   ```java
   MediaPlayer mediaPlayer = new MediaPlayer(context);
   ```

1. 提供框架布局( `android.widget.FrameLayout`)以容纳以下 `ViewGroup` 各项 `mediaPlayer`:

   ```java
   FrameLayout playerFrame = (FrameLayout) _viewGroup.findViewById(R.id.playerFrame);
   ```

   >[!NOTE]
   >
   >以下是要创建的代码片断 `_viewGroup`。

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

   >[!NOTE]
   >
   >实 `MediaPlayer` 例( `mediaPlayer`)现已可用，并正确配置为在设备屏幕上显示视频内容。