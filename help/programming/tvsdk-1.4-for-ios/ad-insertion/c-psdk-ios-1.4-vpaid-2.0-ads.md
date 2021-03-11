---
description: 视频播放器广告服务界面定义(VPAID)2.0提供了播放视频广告的通用界面。 它为用户提供丰富的媒体体验，并允许出版商更好地目标广告、跟踪广告印象和从视频内容受益。
title: VPAID 2.0广告支持
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---


# VPAID 2.0广告支持{#vpaid-ad-support}

视频播放器广告服务界面定义(VPAID)2.0提供了播放视频广告的通用界面。 它为用户提供丰富的媒体体验，并允许出版商更好地目标广告、跟踪广告印象和从视频内容受益。

支持以下功能：

* VPAID规范的2.0版

   有关详细信息，请参阅[IAB VPAID 2.0](https://www.iab.com/wp-content/uploads/2015/06/VPAID_2_0_Final_04-10-2012.pdf)。
* 视频点播(VOD)内容上的线性VPAID广告
* JavaScript VPAID广告

   VPAID广告必须基于JavaScript，且广告响应必须将VPAID广告的媒体类型标识为`application/javascript`。

不支持以下功能：

* VPAID规范的版本1.0
* 可跳过的广告
* 非线性广告，如叠加广告、动态伴侣广告、可最小化广告、可折叠广告和可扩展广告
* 预载VPAID广告
* 实时内容中的VPAID广告
* Flash付费广告
* 滚动后VPAID广告

## API更改{#section_D62F3E059C6C493592D34534B0BFC150}

对API进行了以下更改：

* `PTAuditudeMetadata` 具有一 `customAdLoadTimeout` 个属性，用于更改VPAID加载过程的默认超时。

   默认超时值为10秒。

* `PTMediaPlayerCustomAdNotification` 从实例调 `PTMediaPlayer` 度

<!--<a id="section_495700E1C5404A7B85307A4137C740C5"></a>-->

播放VPAID广告时：

* VPAID广告显示在播放器视图上方的视图容器中，因此依赖用户点击播放器视图的代码不起作用。
* 暂停主内容播放器，并使用对播放器实例上的`pause`和`play`的调用暂停和恢复VPAID广告。

* VPAID广告没有预定义的持续时间，因为该广告可以是交互式广告。

   广告服务器响应定义的广告持续时间和广告中断总持续时间可能不准确。

## 实施VPAID 2.0集成{#section_63C9C737367C4A0AB4D62E0DC2084141}

要在iOS应用程序中添加VPAID 2.0支持，请执行以下操作：

1. （可选）为自定义广告事件添加侦听器。

   ```
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerCustomAdNotification:) name:PTMediaPlayerCustomAdNotification object:self.player];
   ```

1. （可选）显示通知。

   ```
   -(void)onMediaPlayerCustomAdNotification:(NSNotification *)notification{    PTCustomAdNotificationObject *notificationObject = [notification.userInfo objectForKey:PTCustomAdNotificationObjectKey];    if (notificationObject)    
   {        NSLog(@"ViewController:: Custom Ad Notification Received: %ld", notificationObject.type);    } 
   
   }
   ```

