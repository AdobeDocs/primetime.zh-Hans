---
description: 您可以使用Primetime播放器Objective-C API自定义播放器的行为。
title: 媒体播放器类
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---

# 媒体播放器类 {#media-player-classes}

您可以使用Primetime播放器Objective-C API自定义播放器的行为。

这些类描述您的媒体播放器及其资源。

| 类 | 描述 |
|---|---|
| Ptabrcontrolparameters | 封装所有自适应比特率控制参数。 支持的参数包括：<ul><li>minBitRate</li><li>maxBitRate</li><li>初始比特率</li></ul> |
| PTDefaultMediaPlayerClientFactory | TVSDK中PTMediaPlayerClientFactory的默认实施。 它提供availablePTOpportunityResolver、PTContentResolver和PTAdPolicySelector实例。 |
| PTMediaPlayer | 定义Primetime播放器框架的根组件。应用程序创建此类的实例以播放媒体。 此组件会发送通知，让您的应用程序在任何给定时间知道播放器的状态。 |
| PTMediaPlayerClientFactory | 描述自定义媒体播放器客户端工厂应实施哪些方法来提供可用的PTOpportunityResolver 、 PTContentResolver和PTAdPolicySelector实例的协议。 |
| PTMediaPlayerItem | 表示特定的音频 — 视频媒体。 |
| PTMediaPlayerView | 管理Primetime播放器框架的视图组件。 |
| PTMediaProfile | 表示变量播放列表中单个流的配置文件。 |
| PTMediaSelectionOption | 表示一个视听媒体资源，可用于满足不同的语言首选项、辅助功能要求或自定义应用程序配置。 有效的选项类型：<ul><li>字幕(PTMediaSelectionOptionTypeSubtitle)</li><li>备用音频(PTMediaSelectionOptionTypeAudio)</li><li>隐藏式字幕(PTMediaSelectionOptionTypeCC)</li><li>未定义(PTMediaSelectionOptionTypeUndefined)</li></ul> |
| PTOpportunityResolver类，PTOpportunityResolver协议 | 用于处理清单内提示的类，这些提示将用作Adobe Primetime广告决策过程的投放位置。 |
| PTOpportunityResolverDelegate | 描述自定义机会解析器( PTOpportunityResolver )应当用于向委托者传达机会解析状态的协议。 |
| PTSDK | 介绍TVSDK的版本及其功能。 |
| PTSDKConfig | 公开TVSDK全局设置，并允许应用程序订阅自定义HLS标记。 |
| PTTextStyleRule | 定义表示构成规则字典的文本样式属性键的常量。 |
