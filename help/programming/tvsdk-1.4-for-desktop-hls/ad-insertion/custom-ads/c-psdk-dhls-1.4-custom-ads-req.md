---
description: 视频播放器广告服务界面定义(VPAID)为播放视频广告提供了一个通用界面。 VPAID为用户提供了丰富的媒体体验，允许发布者更好地定位广告、跟踪广告展示次数以及从视频内容中盈利。
title: 自定义广告要求
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# 自定义广告要求 {#custom-ad-requirements}

TVSDK播放器可以播放数字视频播放器广告界面定义(VPAID)广告并显示广告加载状态。 如果广告中存在错误，或广告加载时间过长，TVSDK会忽略这些广告。

视频播放器广告服务界面定义(VPAID)为播放视频广告提供了一个通用界面。 VPAID为用户提供了丰富的媒体体验，允许发布者更好地定位广告、跟踪广告展示次数以及从视频内容中盈利。

<!--<a id="section_9A358902CBC24999BA34206EE2029616"></a>-->

TVSDK支持以下功能：

* VPAID规范的1.0和2.0版
* 基于视频点播(VOD)内容的线性VPAID广告
* VPAID广告Flash

  VPAID广告必须基于Flash，广告响应必须将VPAID广告的媒体类型标识为 `application/x-shockwave-flash`.

不支持以下功能：

* 非线性广告，例如叠加广告和动态伴随广告
* 预加载VPAID广告
* 实时内容中的VPAID广告
* JavaScript VPAID广告

## 正在加载状态 {#section_5F55C0101CD44A65BCFE1D124CBDF239}

TVSDK会调度以下事件：

* `AdLoading`
* `AdLoaded`
* `AdStarted`
* `AdPlaying`
* `AdStopped`

在 `AdStopped` 事件，则TVSDK会恢复视频内容。

>[!TIP]
>
>如果指定的值为零，则TVSDK会尝试加载广告，直到广告加载或发生错误为止。

## 忽略广告 {#section_3EA452F420884335AE90DF23C17E416A}

如果广告加载时间过长或广告中存在错误，TVSDK可能会忽略该广告，并且广告面板中的下一个广告会自动播放。

如果 `AuditudeSettings.customAdLoadTimeout` 设置指定大于零的秒数，TVSDK会尝试将广告加载到指定的持续时间。 如果无法加载广告，则会跳过该广告。 例如，如果配置 `AuditudeSettings.customAdLoadTimeout:5`，TVSDK会尝试加载广告，最长时长为5秒。 如果广告仍未加载，则会忽略该广告。
