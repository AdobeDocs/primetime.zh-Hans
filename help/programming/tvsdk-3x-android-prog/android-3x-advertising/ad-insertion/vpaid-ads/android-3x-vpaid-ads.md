---
description: 视频播放器广告服务界面定义(VPAID)2.0提供了播放视频广告的通用界面。 它为用户提供了丰富的媒体体验，使出版商能够更好地定位广告、跟踪广告印象并从视频内容中盈利。
seo-description: 视频播放器广告服务界面定义(VPAID)2.0提供了播放视频广告的通用界面。 它为用户提供了丰富的媒体体验，使出版商能够更好地定位广告、跟踪广告印象并从视频内容中盈利。
seo-title: VPAID 2.0广告支持
title: VPAID 2.0广告支持
uuid: e45e91d2-2aef-4d69-ac80-228d23e8fd7b
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 概述 {#vpaid-ad-support-overview}

视频播放器广告服务界面定义(VPAID)2.0提供了播放视频广告的通用界面。 它为用户提供了丰富的媒体体验，使出版商能够更好地定位广告、跟踪广告印象并从视频内容中盈利。

支持以下功能：

* VPAID规范的2.0版

   有关详细信息，请 [参阅IAB VPAID 2.0](https://www.iab.com/wp-content/uploads/2015/06/VPAID_2_0_Final_04-10-2012.pdf)。
* 具有视频点播(VOD)内容的线性VPAID广告
* JavaScript VPAID广告

   VPAID广告必须基于JavaScript，广告响应必须将VPAID广告的媒体类型标识为 `application/javascript`。

不支持以下功能：

* VPAID规范的版本1.0
* 可跳过的广告
* 非线性广告，如叠加广告、动态伴侣广告、可最小化广告、可折叠广告和可扩展广告
* 预加载VPAID广告
* 实时内容中的VPAID广告
* Flash VPAID广告

## API

以下API元素支持VPAID 2.0广告：

* 返回 `getCustomAdView` 对象的 `MediaPlayer` 方法， `CustomAdView` 表示呈现VPAID广告的Web视图(请参阅 [API引用](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/index.html))。

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` 设置VPAID加载过程的超时。 默认超时值为10秒。

播放VPAID广告时：

* VPAID广告显示在播放器视图上方的视图容器中，因此依赖于用户在播放器视图上点击的代码不起作用。
* 对播放 `pause` 器实 `play` 例的调用暂停并恢复VPAID广告。

* VPAID广告没有预定义的持续时间，因为广告可以是交互式的。

   广告服务器响应中指定的广告持续时间和广告中断总持续时间可能不准确。