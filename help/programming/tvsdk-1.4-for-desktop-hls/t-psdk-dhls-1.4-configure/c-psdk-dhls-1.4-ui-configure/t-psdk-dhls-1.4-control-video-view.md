---
description: 您可以使用MediaPlayerView对象控制视频视图的位置和大小。
title: 控制视频视图的位置和大小
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# 控制视频视图的位置和大小{#control-the-position-and-size-of-the-video-view}

您可以使用MediaPlayerView对象控制视频视图的位置和大小。

默认情况下，TVSDK会在视频的大小或位置发生更改（由于应用程序、配置文件开关或内容开关等所做的更改）时，尝试保持视频视图的长宽比。

可通过指定其他参数来覆盖缺省纵横比行为 *缩放策略*. 使用指定缩放策略 `MediaPlayerView` 对象的 `scalePolicy` 属性。 此 `MediaPlayerView`的默认缩放策略通过 `MaintainAspectRatioScalePolicy` 类。 要重置缩放策略，请替换默认实例 `MaintainAspectRatioScalePolicy` 日期 `MediaPlayerView.scalePolicy` 你自己的政策。 (您无法设置 `scalePolicy` 属性转换为null值。)

1. 实施 `MediaPlayerViewScalePolicy` 界面创建您自己的扩展策略。

   此 `MediaPlayerViewScalePolicy` 具有一种方法：

   ```
   public function adjust(viewPort:Rectangle, 
     videoWidth:Number, videoHeight:Number):Rectangle;
   ```

   >[!NOTE]
   >
   >TVSDK使用 `StageVideo` 用于显示视频的对象，并且 `StageVideo` 对象不在显示列表中， `viewPort` 参数包含视频的绝对坐标。
   >
   >
   >例如：
   >
   >```
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
   >```
   >

1. 将您的实施分配给 `MediaPlayerView` 属性。

   ```
   var view:MediaPlayerView = MediaPlayerView.create(stage.stageVideos[0]); 
   view.scalePolicy = new CustomScalePolicy();
   ```

1. 将视图添加到媒体播放器的 `view` 属性。

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
