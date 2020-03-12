---
description: 您可以使用MediaPlayerView对象控制视频视图的位置和大小。
seo-description: 您可以使用MediaPlayerView对象控制视频视图的位置和大小。
seo-title: 控制视频视图的位置和大小
title: 控制视频视图的位置和大小
uuid: 2231c574-03cd-45a8-ab00-4a42f8e044f0
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 控制视频视图的位置和大小{#control-the-position-and-size-of-the-video-view}

您可以使用MediaPlayerView对象控制视频视图的位置和大小。

默认情况下，每当视频的大小或位置发生变化时（由于应用程序、配置文件开关或内容开关等的更改）,TVSDK都会尝试保持视频视图的宽高比。

您可以通过指定其他缩放策略来覆盖默认的宽高比 *行为*。 使用对象的属性指 `MediaPlayerView` 定缩放策 `scalePolicy` 略。 默认 `MediaPlayerView`的缩放策略是使用类的一个实例设 `MaintainAspectRatioScalePolicy` 置的。 要重置比例策略，请用您自己的策略替换 `MaintainAspectRatioScalePolicy` on的 `MediaPlayerView.scalePolicy` 默认实例。 (不能将该属 `scalePolicy` 性设置为null值。)

1. 实现该 `MediaPlayerViewScalePolicy` 接口以创建您自己的缩放策略。

   它有 `MediaPlayerViewScalePolicy` 一种方法：

   ```
   public function adjust(viewPort:Rectangle, 
     videoWidth:Number, videoHeight:Number):Rectangle;
   ```

   >[!NOTE]
   >
   >TVSDK使用对 `StageVideo` 象来显示视频，并且由于对 `StageVideo` 象不在显示列表中，因此该参数 `viewPort` 包含视频的绝对坐标。
   >
   >
   >例如：   >
   >
   >
   ```>
   >public class CustomScalePolicy implements MediaPlayerViewScalePolicy { 
   >       /** 
   >         * Default constructor. 
   >         */ 
   >       public function CustomScalePolicy() { 
   >       } 
   > 
   >    
      public function adjust(viewPort:Rectangle,  
   >                                                     videoWidth:Number,  
   >                                                     videoHeight:Number):Rectangle { 
   >               return customAdjustment(); 
   >       } 
   > 
   >    
      public function customAdjustment():Rectangle { 
   >               /* Your custom adjustment here */ 
   >               [...] 
   >       } 
   >}
   >```   >
   >



1. 将您的实施分配给该 `MediaPlayerView` 属性。

   ```
   var view:MediaPlayerView = MediaPlayerView.create(stage.stageVideos[0]); 
   view.scalePolicy = new CustomScalePolicy();
   ```

1. 将您的视图添加到Media Player的属 `view` 性。

   ```
   addChild(view); 
   
   mediaPlayer.view = view;
   ```

<!--<a id="example_7B08ECCDA17B4DD191FC672BD1F4C850"></a>-->

**例如：缩放视频以填充整个视频视图，而不保持宽高比：**

```
package com.adobe.mediacore.samples.utils { 
    import com.adobe.mediacore.view.MediaPlayerViewScalePolicy; 
    import flash.geom.Rectangle; 
 
    /** 
    * A very simple custom scale policy - the video will fill the entire 
    * allocated space. The aspect ratio will not be kept. 
    */ 
    public class CustomScalePolicy implements MediaPlayerViewScalePolicy { 
 
        /** 
        * Default constructor. 
        */ 
        public function CustomScalePolicy() { 
        } 
 
        public function adjust(viewPort:Rectangle, 
                               videoWidth:Number,  
                               videoHeight:Number):Rectangle { 
            return viewPort; 
        } 
    } 
} 
 
var view:MediaPlayerView = MediaPlayerView.create(stage.stageVideos[0]); 
view.scalePolicy = new CustomScalePolicy(); 
addChild(view); 
mediaPlayer.view = view;
```

