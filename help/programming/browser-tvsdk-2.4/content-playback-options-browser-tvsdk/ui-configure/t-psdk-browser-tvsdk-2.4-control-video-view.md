---
description: 您可以使用MediaPlayerView对象控制视频视图的位置和大小。
seo-description: 您可以使用MediaPlayerView对象控制视频视图的位置和大小。
seo-title: 控制视频视图的位置和大小
title: 控制视频视图的位置和大小
uuid: d09dbc18-1ec0-4336-bf3f-7ff6c265c443
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 控制视频视图的位置和大小{#control-the-position-and-size-of-the-video-view}

您可以使用MediaPlayerView对象控制视频视图的位置和大小。

默认情况下，当视频的大小或位置因应用程序、配置文件切换、内容切换等所做的更改而发生变化时，浏览器TVSDK会尝试保持视频视图的宽高比。

您可以通过指定其他缩放策略来覆盖默认的宽高比 *行为*。 使用对象的属性指 `MediaPlayerView` 定缩放策 `scalePolicy` 略。 默认的缩放策 `MediaPlayerView` 略是使用类的一个实例设 `MaintainAspectRatioScalePolicy` 置的。 要重置比例策略，请用您自己的策略替换 `MaintainAspectRatioScalePolicy` on的 `MediaPlayerView.scalePolicy` 默认实例。

>[!IMPORTANT]
>
>不能将该属 `scalePolicy` 性设置为null值。

## 非Flash备用方案 {#non-flash-fallback-scenarios}

在非Flash备用场景中，为了使缩放策略能够正确工作，构造函数中给定的视频div元素应 `View` 为和返回非零 `offsetWidth` 值 `offsetHeight`。 为了给出一个错误函数的示例，有时当视频div元素的宽度和高度未在css中显式设置时，构造函数 `View` 为或返回 `offsetWidth` 零 `offsetHeight`。

>[!NOTE]
>
>CustomScalePolicy对一些浏览器（特别是IE、Edge和Safari 9）的支持有限。 对于这些浏览器，无法更改视频的本机长宽比。 但是，视频的位置和尺寸将根据缩放策略实施。

1. 实现该 `MediaPlayerViewScalePolicy` 接口以创建您自己的缩放策略。

   它有 `MediaPlayerViewScalePolicy` 一种方法：

   ```js
   /** 
   * Adjust the specified rectangle to match the new video dimensions. 
   * @param viewPort {AdobePSDK.Rectangle}The video rectangle as absolute position. 
   * @param videoWidth {Number}The video width. 
   * @param videoHeight {Number} The video height. 
   * @return {AdobePSDK.Rectangle} an adjusted rectangle. 
   */ 
   function adjustCallbackFunc(viewPort, videoWidth, videoHeight);
   ```

   例如：

   ```js
   /** 
   Default Constructor 
   */ 
   MediaPlayerViewCustomScalePolicy = function() { 
       return this; 
   }; 
   MediaPlayerViewCustomScalePolicy.prototype = { 
       constructor: MediaPlayerViewScalePolicy, 
       adjustCallbackFunc: function(viewPort, videoWidth, videoHeight) { 
           /* Your Custom Adjustment here. */ 
           [...] 
           return adjustedRectangle; 
       } 
   };
   ```

1. 将您的实施分配给该 `MediaPlayerView` 属性。

   ```js
   var view = new AdobePSDK.MediaPlayerView(videoDiv); 
   view.scalePolicy= new MediaPlayerViewCustomScalePolicy();
   ```

1. 将您的视图添加到Media Player的属 `view` 性。

   ```
   mediaplayer.view = view;
   ```

<!--<a id="example_ABCD79AE29DB4A668F9A8B729FE44AF9"></a>-->

**例如：缩放视频以填充整个视频视图，而不保持宽高比：**

```
/** 
 * Default constructor. 
 */ 
MediaPlayerViewCustomScalePolicy = function() { 
    return this; 
}; 
MediaPlayerViewCustomScalePolicy.prototype = { 
    constructor: MediaPlayerViewScalePolicy, 
    /** 
    * A very simple custom scale policy - the video will fill the entire 
    * allocated space. The aspect ratio will not be kept. 
    */ 
    adjustCallbackFunc: function(viewPort, videoWidth, videoHeight) { 
        return viewPort; 
    } 
}; 
var view = new AdobePSDK.MediaPlayerView(videoDiv); 
view.scalePolicy = new MediaPlayerViewCustomScalePolicy (); 
mediaPlayer.view = view;
```

