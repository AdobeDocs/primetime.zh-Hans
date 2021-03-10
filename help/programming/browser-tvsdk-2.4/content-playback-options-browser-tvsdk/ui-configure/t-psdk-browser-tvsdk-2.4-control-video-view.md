---
description: 您可以使用MediaPlayerView对象控制视频视图的位置和大小。
title: 控制视频视图的位置和大小
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---


# 控制视频视图的位置和大小{#control-the-position-and-size-of-the-video-view}

您可以使用MediaPlayerView对象控制视频视图的位置和大小。

默认情况下，当视图的大小或位置因应用程序、用户档案开关、内容开关等所做的更改而发生变化时，浏览器TVSDK会尝试保持视频的宽高比。

可以通过指定不同的&#x200B;*缩放策略*&#x200B;来覆盖默认的宽高比行为。 使用`MediaPlayerView`对象的`scalePolicy`属性指定缩放策略。 使用`MaintainAspectRatioScalePolicy`类的实例设置`MediaPlayerView`的默认缩放策略。 要重置缩放策略，请将`MediaPlayerView.scalePolicy`上`MaintainAspectRatioScalePolicy`的默认实例替换为您自己的策略。

>[!IMPORTANT]
>
>不能将`scalePolicy`属性设置为null值。

## 非Flash回退方案{#non-flash-fallback-scenarios}

在非Flash回退方案中，要使缩放策略正常工作，`View`构造函数中提供的视频div元素应返回`offsetWidth`和`offsetHeight`的非零值。 要给出一个不正确函数的示例，有时当视频div元素的宽度和高度未在css中显式设置时，`View`构造函数会为`offsetWidth`或`offsetHeight`返回零。

>[!NOTE]
>
>CustomScalePolicy对一些浏览器（尤其是IE、Edge和Safari 9）的支持有限。 对于这些浏览器，无法更改视频的本机长宽比。 但是，视频的位置和尺寸将根据缩放策略强制执行。

1. 实现`MediaPlayerViewScalePolicy`接口以创建您自己的缩放策略。

   `MediaPlayerViewScalePolicy`有一种方法：

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

1. 将实现分配给`MediaPlayerView`属性。

   ```js
   var view = new AdobePSDK.MediaPlayerView(videoDiv); 
   view.scalePolicy= new MediaPlayerViewCustomScalePolicy();
   ```

1. 将您的视图添加到Media Player的`view`属性。

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

