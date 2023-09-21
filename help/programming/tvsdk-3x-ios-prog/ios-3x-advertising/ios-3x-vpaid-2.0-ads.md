---
description: 视频播放器广告服务界面定义(VPAID) 2.0提供了一个用于播放视频广告的通用界面。 它为用户提供了丰富的媒体体验，允许发布者更好地定位广告、跟踪广告展示次数以及从视频内容中盈利。
title: VPAID 2.0广告支持
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# VPAID 2.0广告支持 {#vpaid-ad-support}

视频播放器广告服务界面定义(VPAID) 2.0提供了一个用于播放视频广告的通用界面。 它为用户提供了丰富的媒体体验，允许发布者更好地定位广告、跟踪广告展示次数以及从视频内容中盈利。

支持以下功能：

* VPAID规范版本2.0

  有关更多信息，请参阅 [IAB VPAID 2.0](https://www.iab.com/wp-content/uploads/2015/06/VPAID_2_0_Final_04-10-2012.pdf).
* 基于视频点播(VOD)内容的线性VPAID广告
* JavaScript VPAID广告

  VPAID广告必须基于JavaScript，广告响应必须将VPAID广告的媒体类型标识为 `application/javascript`.

不支持以下功能：

* VPAID规范版本1.0
* 可跳过广告
* 非线性广告，例如叠加广告、动态伴随广告、可最小化广告、可折叠广告和可展开广告
* 预加载VPAID广告
* 实时内容中的VPAID广告
* VPAID广告Flash
* 后置式VPAID广告

## API更改 {#section_D62F3E059C6C493592D34534B0BFC150}

对API进行了以下更改：

* `PTAuditudeMetadata` 具有 `customAdLoadTimeout` 属性，用于更改VPAID加载过程中的默认超时。

  默认超时值为10秒。

* `PTMediaPlayerCustomAdNotification` 是从 `PTMediaPlayer` 实例

<!--<a id="section_495700E1C5404A7B85307A4137C740C5"></a>-->

当VPAID广告正在播放时：

* VPAID广告显示在播放器视图上方的视图容器中，因此依赖播放器视图上的用户点按的代码不起作用。
* 主内容播放器已暂停，并调用 `pause` 和 `play` 播放器实例上的内容用于暂停和恢复VPAID广告。

* VPAID广告没有预定义的持续时间，因为广告可以是交互式的。

  由广告服务器响应定义的广告持续时间和广告时间总持续时间可能不准确。

## 实施VPAID 2.0集成 {#section_63C9C737367C4A0AB4D62E0DC2084141}

要在您的iOS应用程序中添加VPAID 2.0支持，请执行以下操作：

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
