---
description: 您可以使用MediaPlayerView对象控制视频视图的位置和大小。
title: 控制视频视图的位置和大小
exl-id: ab88a90f-4493-4f05-8da0-703ab3cf159e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# 控制视频视图的位置和大小{#control-the-position-and-size-of-the-video-view}

您可以使用MediaPlayerView对象控制视频视图的位置和大小。

默认情况下，每当视频的大小或位置因应用程序、配置文件开关、内容开关等所做的更改而改变时，浏览器TVSDK会尝试保持视频视图的长宽比。

可通过指定其他参数来覆盖缺省的长宽比行为 *缩放策略*. 使用指定缩放策略 `MediaPlayerView` 对象的 `scalePolicy` 属性。 默认缩放策略 `MediaPlayerView` 使用的一个实例设置的 `MaintainAspectRatioScalePolicy` 类。 要重置缩放策略，请替换默认实例 `MaintainAspectRatioScalePolicy` 日期 `MediaPlayerView.scalePolicy` 你自己的政策。

>[!IMPORTANT]
>
>您无法设置 `scalePolicy` 属性转换为null值。

## 非Flash回退方案 {#non-flash-fallback-scenarios}

在非Flash回退方案中，为了使scale策略正常工作，在中给定的视频div元素 `View` 构造函数应返回非零值 `offsetWidth` 和 `offsetHeight`. 要给出不正确函数的示例，有时当视频div元素的宽度和高度未在css中显式设置时，则 `View` 构造函数为 `offsetWidth` 或 `offsetHeight`.

>[!NOTE]
>
>CustomScalePolicy对几种浏览器（特别是IE、Edge和Safari 9）的支持有限。 对于这些浏览器，无法更改视频的本机纵横比。 但是，视频的位置和维度将根据缩放策略执行。

1. 实施 `MediaPlayerViewScalePolicy` 界面创建您自己的缩放策略。

   此 `MediaPlayerViewScalePolicy` 具有一种方法：

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

1. 将您的实施分配给 `MediaPlayerView` 属性。

   ```js
   var view = new AdobePSDK.MediaPlayerView(videoDiv); 
   view.scalePolicy= new MediaPlayerViewCustomScalePolicy();
   ```

1. 将视图添加到媒体播放器的 `view` 属性。

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
