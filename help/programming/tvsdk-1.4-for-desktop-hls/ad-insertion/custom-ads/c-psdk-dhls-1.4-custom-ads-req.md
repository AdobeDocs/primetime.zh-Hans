---
description: 视频播放器广告服务界面定义(VPAID)提供了播放视频广告的通用界面。 VPAID为用户提供丰富的媒体体验，使出版商能够更好地目标广告、跟踪广告印象并从视频内容受益。
seo-description: 视频播放器广告服务界面定义(VPAID)提供了播放视频广告的通用界面。 VPAID为用户提供丰富的媒体体验，使出版商能够更好地目标广告、跟踪广告印象并从视频内容受益。
seo-title: 自定义广告要求
title: 自定义广告要求
uuid: 6d4ba87b-ffe5-467d-8ab5-9795928c2f69
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 0%

---


# 自定义广告要求{#custom-ad-requirements}

TVSDK播放器可播放数字视频播放器广告界面定义(VPAID)广告并显示广告加载状态。 如果广告中有错误，或广告加载时间过长，TVSDK将忽略这些广告。

视频播放器广告服务界面定义(VPAID)提供了播放视频广告的通用界面。 VPAID为用户提供丰富的媒体体验，使出版商能够更好地目标广告、跟踪广告印象并从视频内容受益。

<!--<a id="section_9A358902CBC24999BA34206EE2029616"></a>-->

TVSDK支持以下功能：

* VPAID规范的版本1.0和2.0
* 视频点播(VOD)内容上的线性VPAID广告
* FlashVPAID广告

   VPAID广告必须基于Flash，广告响应必须将VPAID广告的媒体类型标识为`application/x-shockwave-flash`。

不支持以下功能：

* 叠加广告和动态伴侣广告等非线性广告
* 预载VPAID广告
* 实时内容中的VPAID广告
* JavaScript VPAID广告

## 正在加载状态{#section_5F55C0101CD44A65BCFE1D124CBDF239}

TVSDK发送以下事件:

* `AdLoading`
* `AdLoaded`
* `AdStarted`
* `AdPlaying`
* `AdStopped`

在`AdStopped`事件后，TVSDK恢复视频内容。

>[!TIP]
>
>如果指定值为零，则TVSDK将尝试加载广告，直到它加载或出现错误。

## 忽略广告{#section_3EA452F420884335AE90DF23C17E416A}

如果加载广告需要太长时间或广告中有错误，TVSDK可以忽略该广告，并自动播放广告窗格中的下一个广告。

如果`AuditudeSettings.customAdLoadTimeout`设置指定的秒数大于零，则TVSDK将尝试将广告加载到指定的持续时间。 如果无法加载广告，则会跳过广告。 例如，如果配置`AuditudeSettings.customAdLoadTimeout:5`,TVSDK将尝试加载广告最多5秒。 如果广告仍未加载，则忽略该广告。
