---
description: 视频播放器广告服务界面定义(VPAID) 2.0提供了一个用于播放视频广告的通用界面。 它为用户提供了丰富的媒体体验，允许发布者更好地定位广告、跟踪广告展示次数以及从视频内容中盈利。
title: VPAID 2.0广告支持
exl-id: ee3e0cd9-463e-4de9-a94f-292e968b6f08
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '384'
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

* VPAID规范的1.0版
* 可跳过广告
* 非线性广告，例如叠加广告、动态伴随广告、可最小化广告、可折叠广告和可展开广告
* 预加载VPAID广告
* 实时内容中的VPAID广告
* VPAID广告Flash

## API更改 {#section_D62F3E059C6C493592D34534B0BFC150}

对API进行了以下更改：

* A `getCustomAdView` 函数已添加到 `MediaPlayer` 并返回渲染VPAID广告的Web视图。

   欲知关于 `CustomAdView` 此函数返回的对象，请参见 [API引用](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/index.html).

* A `CUSTOM_AD` 事件是从媒体播放器实例中调度的。

   该应用程序可以通过以下方式注册事件回调： `CustomAdEventListener`.

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` 允许您更改VPAID加载过程的默认超时。

   默认超时值为10秒。

<!--<a id="section_495700E1C5404A7B85307A4137C740C5"></a>-->

播放VPAID广告时：

* VPAID广告显示在播放器视图上方的视图容器中，因此依赖播放器视图上的用户点按的代码不起作用。
* 主内容播放器已暂停，并调用 `pause` 和 `play` ，用于暂停和恢复VPAID广告。

* VPAID广告没有预定义的持续时间，因为广告可以是交互式的。

   由广告服务器响应定义的广告持续时间和广告时间总持续时间可能不准确。

## 实施VPAID 2.0集成 {#implement-vpaid-integration}

要添加VPAID 2.0支持，请添加自定义广告视图和适当的侦听器。

要添加VPAID 2.0支持，请执行以下操作：

1. 将自定义广告视图添加到播放器界面。

   ```java
   _playerFrame.addView(mediaPlayer.createCustomAdView());
   ```

1. 为自定义广告事件添加侦听器。

   ```java
   mediaplayer.addEventListener(MediaPlayer.Event.CUSTOM_AD,  
     _customAdEventListener);
   ```
