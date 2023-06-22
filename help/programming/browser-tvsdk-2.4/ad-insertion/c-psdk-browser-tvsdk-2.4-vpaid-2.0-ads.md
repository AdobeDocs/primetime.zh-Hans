---
description: 视频播放器广告服务界面定义(VPAID) 2.0提供了用于播放视频广告的通用界面。 它为用户提供了丰富的媒体体验，允许发布者更好地定位广告、跟踪广告展示次数以及从视频内容中盈利。
title: VPAID 2.0广告支持
exl-id: ea3dcd1d-c4e2-46c6-b613-e86c3e161ca8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# VPAID 2.0广告支持 {#vpaid-ad-support}

视频播放器广告服务界面定义(VPAID) 2.0提供了用于播放视频广告的通用界面。 它为用户提供了丰富的媒体体验，允许发布者更好地定位广告、跟踪广告展示次数以及从视频内容中盈利。

支持以下功能：

* VPAID规范版本2.0

   有关更多信息，请参阅 [IAB VPAID 2.0](https://www.iab.com/guidelines/digital-video-player-ad-interface-definition-vpaid-2-0/).
* 包含视频点播(VOD)内容的线性VPAID广告
* 在实时内容中，浏览器TVSDK支持前置式JavaScript VPAID广告。
* 在Flash回退模式下，Browser TVSDK仅支持基于Flash的VPAID广告。
* 线性JavaScript VPAID广告

   VPAID广告必须基于JavaScript，广告响应必须将VPAID广告的媒体类型标识为 `application/javascript`.

不支持以下功能：

* VPAID规范的1.0版
* 可跳过广告
* 非线性广告，例如叠加广告、动态伴随广告、可最小化广告、可折叠广告和可展开广告。
* 预加载VPAID广告
* 实时内容中的VPAID广告
* VPAID广告Flash

## API {#section_0DB1D383CA5047B281BC808BC082C69B}

以下API元素支持VPAID 2.0广告：

* 此 `getCustomAdView` 方法 `MediaPlayer` 返回 `CustomAdView` 对象，表示渲染VPAID广告的Web视图。

   欲知关于 `getCustomAdView` 方法，请参见 [MediaPlayer API文档](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/AdobePSDK.MediaPlayer.html).

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` 在VPAID加载过程中设置超时。

   默认超时值为10秒。

* API、 `auditudeSettings.ignoreVPAIDAds`，用于忽略从Auditude服务器接收的VPAID广告。 该API不适用于Flash回退。

播放VPAID广告时：

* VPAID广告显示在播放器视图上方的视图容器中，因此依赖播放器视图上的用户点按的代码不起作用。
* 在播放器实例上暂停和播放并恢复VPAID广告的调用。
* VPAID广告没有预定义的持续时间，因为广告可以是交互式的。

   在广告服务器响应中指定的广告持续时间和广告时间总持续时间可能不准确。
