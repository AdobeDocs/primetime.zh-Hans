---
description: TVSDK支持在广告中断时显示线性视频播放器——广告界面定义(VPAID)广告。 VPAID版本1.0需要Flash，而版本2.0也可与浏览器TVSDK和JavaScript一起使用。
seo-description: TVSDK支持在广告中断时显示线性视频播放器——广告界面定义(VPAID)广告。 VPAID版本1.0需要Flash，而版本2.0也可与浏览器TVSDK和JavaScript一起使用。
seo-title: 在广告时段显示线性VPAID广告
title: 在广告时段显示线性VPAID广告
uuid: 1f3a5426-79f5-49a1-a913-923708c09ade
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---


# 在广告时段显示线性VPAID广告{#display-linear-vpaid-ads-in-an-ad-break}

TVSDK支持在广告中断时显示线性视频播放器——广告界面定义(VPAID)广告。 VPAID版本1.0需要Flash，而版本2.0也可与浏览器TVSDK和JavaScript一起使用。

要正确显示VPAID广告，您必须在`MediaPlayerContext`实例中提供广告容器(`AdContainerView`)。

VPAID广告的限制：

* VPAID广告不一定具有预定义的持续时间，因为广告可以是交互式广告。 因此，广告持续时间（由广告服务器响应定义）可能并不总是与广告的真实持续时间完全对应。
* 对于VPAID 1.0广告，TVSDK要求在设备上安装Flash播放器14.0.0.160或更高版本。 对于Flash播放器的早期版本，此功能被禁用，并跳过VPAID 1.0广告。

要设置广告容器以在广告分时段内显示VPAID广告（版本1.0或2.0），请执行以下操作：

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

1. 调整视图大小时，重置广告容器的大小。

   ```
   adContainer.setSize(stage.stageWidth, stage.stageHeight);
   ```

   >[!NOTE]
   >
   >当您获得全屏更改事件并在广告容器上设置新大小时，按如下方式传递舞台显示状态以确保播放器正确调整大小：
   >
   >
   ```
   >private function onFullScreenChange(event:FullScreenEvent):void { 
   >if (_adContainer) 
   >{ _adContainer.setSize(stage.stageWidth, stage.stageHeight, stage.displayState); } 
   >}
   >```

