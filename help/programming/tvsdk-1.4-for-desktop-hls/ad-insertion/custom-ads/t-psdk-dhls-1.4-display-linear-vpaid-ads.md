---
description: TVSDK支持在广告时间显示线性视频播放器广告界面定义(VPAID)广告。 VPAID版本1.0需要Flash，而版本2.0也可以与浏览器TVSDK和JavaScript一起使用。
title: 在广告时间显示线性VPAID广告
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# 在广告时间显示线性VPAID广告{#display-linear-vpaid-ads-in-an-ad-break}

TVSDK支持在广告时间显示线性视频播放器广告界面定义(VPAID)广告。 VPAID版本1.0需要Flash，而版本2.0也可以与浏览器TVSDK和JavaScript一起使用。

要正确显示VPAID广告，您必须提供广告容器( `AdContainerView`)中 `MediaPlayerContext` 实例。

VPAID广告的限制：

* 鉴于广告可以是交互式的，VPAID广告不一定具有预定义的持续时间。 因此，广告持续时间（由广告服务器响应定义）可能并不总是完全对应于广告的真实持续时间。
* 对于VPAID 1.0广告，TVSDK要求在设备上安装Flash播放器14.0.0.160或更高版本。 对于Flash播放器的早期版本，此功能已禁用，并跳过VPAID 1.0广告。

要设置广告容器以在广告时间显示VPAID广告（版本1.0或2.0），请执行以下操作：

1. 使用以下示例代码设置可显示VPAID广告的广告容器。

   ```
   var context:MediaPlayerContext =  
     new MediaPlayerContext(_authorizedFeatureHelper.authorizedFeatures); 
   
   adContainer = new AdContainerView(); 
   adContainer.x = adContainer.y = 0; 
   adContainer.setSize(videoContainer.width, videoContainer.height); 
   addChild(adContainer); 
   
   context.adContainer = adContainer; 
   _player = new DefaultMediaPlayer(context);
   ```

1. 当视图调整大小时，重置广告容器上的大小。

   ```
   adContainer.setSize(stage.stageWidth, stage.stageHeight);
   ```

   >[!NOTE]
   >
   >当您收到全屏更改事件并在广告容器中设置新大小时，请按照以下方式传递舞台显示状态，以确保播放器正确调整大小：
   >
   >```
   >private function onFullScreenChange(event:FullScreenEvent):void { 
   >if (_adContainer) 
   >{ _adContainer.setSize(stage.stageWidth, stage.stageHeight, stage.displayState); } 
   >}
   >```
   >
