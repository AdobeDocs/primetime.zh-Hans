---
description: 视频播放器广告服务界面定义(VPAID)2.0提供了播放视频广告的通用界面。 它为用户提供了丰富的媒体体验，使出版商能够更好地定位广告、跟踪广告印象并从视频内容中盈利。
seo-description: 视频播放器广告服务界面定义(VPAID)2.0提供了播放视频广告的通用界面。 它为用户提供了丰富的媒体体验，使出版商能够更好地定位广告、跟踪广告印象并从视频内容中盈利。
seo-title: VPAID 2.0广告支持
title: VPAID 2.0广告支持
uuid: 7168a6e4-9c5e-4d3a-8710-867cf98e4445
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# VPAID 2.0广告支持 {#vpaid-ad-support}

视频播放器广告服务界面定义(VPAID)2.0提供了播放视频广告的通用界面。 它为用户提供了丰富的媒体体验，使出版商能够更好地定位广告、跟踪广告印象并从视频内容中盈利。

支持以下功能：

* VPAID规范的2.0版

   有关详细信息，请 [参阅IAB VPAID 2.0](https://www.iab.com/wp-content/uploads/2015/06/VPAID_2_0_Final_04-10-2012.pdf)。
* 视频点播(VOD)内容上的线性VPAID广告
* JavaScript VPAID广告

   VPAID广告必须基于JavaScript，广告响应必须将VPAID广告的媒体类型标识为 `application/javascript`。

不支持以下功能：

* VPAID规范的版本1.0
* 可跳过的广告
* 非线性广告，如叠加广告、动态伴侣广告、可最小化广告、可折叠广告和可扩展广告
* 预加载VPAID广告
* 实时内容中的VPAID广告
* Flash VPAID广告

## API更改 {#section_D62F3E059C6C493592D34534B0BFC150}

对API进行了以下更改：

* 已 `getCustomAdView` 在中添加一个函数， `MediaPlayer` 并返回呈现VPAID广告的Web视图。

   有关此函数返 `CustomAdView` 回的对象的详细信息，请参阅 [API引用](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/index.html)。

* 从媒 `CUSTOM_AD` 体播放器实例中调度事件。

   应用程序可以通过实现来注册事件回调 `CustomAdEventListener`。

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` 允许您在VPAID加载过程中更改默认超时。

   默认超时值为10秒。

<!--<a id="section_495700E1C5404A7B85307A4137C740C5"></a>-->

播放VPAID广告时：

* VPAID广告显示在播放器视图上方的视图容器中，因此依赖于用户在播放器视图上点击的代码不起作用。
* 主内容播放器暂停，并且对播放器实 `pause` 例的 `play` 调用用于暂停和恢复VPAID广告。

* VPAID广告没有预定义的持续时间，因为广告可以是交互式的。

   广告服务器响应定义的广告持续时间和广告中断总持续时间可能不准确。

## 实施VPAID 2.0集成 {#implement-vpaid-integration}

要添加VPAID 2.0支持，请添加自定义广告视图和相应的监听器。

要添加VPAID 2.0支持，请执行以下操作：

1. 将自定义广告视图添加到播放器界面。

   ```java
   _playerFrame.addView(mediaPlayer.createCustomAdView());
   ```

1. 为自定义广告事件添加监听器。

   ```java
   mediaplayer.addEventListener(MediaPlayer.Event.CUSTOM_AD,  
     _customAdEventListener);
   ```
