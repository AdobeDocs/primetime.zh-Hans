---
description: 视频播放器广告服务界面定义(VPAID)2.0提供了播放视频广告的通用界面。 它为用户提供了丰富的媒体体验，使出版商能够更好地定位广告、跟踪广告印象并从视频内容中盈利。
seo-description: 视频播放器广告服务界面定义(VPAID)2.0提供了播放视频广告的通用界面。 它为用户提供了丰富的媒体体验，使出版商能够更好地定位广告、跟踪广告印象并从视频内容中盈利。
seo-title: VPAID 2.0广告支持
title: VPAID 2.0广告支持
uuid: 462692b5-c4b3-4488-adb3-f309809d64ad
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# VPAID 2.0广告支持 {#vpaid-ad-support}

视频播放器广告服务界面定义(VPAID)2.0提供了播放视频广告的通用界面。 它为用户提供了丰富的媒体体验，使出版商能够更好地定位广告、跟踪广告印象并从视频内容中盈利。

支持以下功能：

* VPAID规范的2.0版

   有关详细信息，请 [参阅IAB VPAID 2.0](https://www.iab.com/guidelines/digital-video-player-ad-interface-definition-vpaid-2-0/)。
* 具有视频点播(VOD)内容的线性VPAID广告
* 在实时内容中，浏览器TVSDK支持预先发布的JavaScript VPAID广告。
* 在Flash回退模式中，浏览器TVSDK仅支持基于Flash的VPAID广告。
* 线性JavaScript VPAID广告

   VPAID广告必须基于JavaScript，广告响应必须将VPAID广告的媒体类型标识为 `application/javascript`。

不支持以下功能：

* VPAID规范的版本1.0
* 可跳过的广告
* 非线性广告，如叠加广告、动态伴侣广告、可最小化广告、可折叠广告和可扩展广告。
* 预加载VPAID广告
* 实时内容中的VPAID广告
* Flash VPAID广告

## API {#section_0DB1D383CA5047B281BC808BC082C69B}

以下API元素支持VPAID 2.0广告：

* 返回 `getCustomAdView` 对象的 `MediaPlayer` 方法， `CustomAdView` 该对象表示呈现VPAID广告的Web视图。

   有关该方法的更多 `getCustomAdView` 信息，请参 [阅MediaPlayer API文档](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/AdobePSDK.MediaPlayer.html)。

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` 设置VPAID加载过程的超时。

   默认超时值为10秒。

* 该API允 `auditudeSettings.ignoreVPAIDAds`许您忽略从Auditude服务器收到的VPAID广告。 该API不适用于Flash备份。

播放VPAID广告时：

* VPAID广告显示在播放器视图上方的视图容器中，因此依赖于用户在播放器视图上点击的代码不起作用。
* 暂停和播放播放器实例暂停和继续VPAID广告的调用。
* VPAID广告没有预定义的持续时间，因为广告可以是交互式的。

   广告服务器响应中指定的广告持续时间和广告中断总持续时间可能不准确。