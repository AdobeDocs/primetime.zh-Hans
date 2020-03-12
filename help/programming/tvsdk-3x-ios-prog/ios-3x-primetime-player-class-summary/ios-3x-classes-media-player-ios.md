---
description: 您可以使用Primetime Player Objective-C API自定义播放器的行为。
seo-description: 您可以使用Primetime Player Objective-C API自定义播放器的行为。
seo-title: 媒体播放器类
title: 媒体播放器类
uuid: 705c71b6-4e5e-46b5-a59d-13df977b04f2
translation-type: tm+mt
source-git-commit: b13f2d3f083a6ca333a4edba1c8d7261f7d448ad

---


# 媒体播放器类 {#media-player-classes}

您可以使用Primetime Player Objective-C API自定义播放器的行为。

这些类描述您的媒体播放器及其资源。

| 类 | 说明 |
|---|---|
| PTABRControlParameters | 封装所有自适应比特率控制参数。 支持的参数有：<ul><li>minBitRate</li><li>maxBitRate</li><li>initialBitRate</li></ul> |
| PTDefaultMediaPlayerClientFactory | 在TVSDK中默认实现PTMediaPlayerClientFactory。 它提供了availablePTOpportunityResolver、PTContentResolver和PTAdPolicySelector实例。 |
| PTMediaPlayer | 定义Primetime Player框架的根组件。应用程序创建该类的一个实例以回放媒体。 此组件会发送通知，让应用程序知道播放器在任何给定时间的状态。 |
| PTMediaPlayerClientFactory | 描述自定义媒体播放器客户端工厂应实施的方法以提供可用的PTOpportunityResolver、PTContentResolver和PTAdPolicySelector实例的协议。 |
| PTMediaPlayerItem | 表示特定的音频——视频媒体。 |
| PTMediaPlayerView | 管理Primetime Player框架的视图组件。 |
| PTMediaProfile | 表示变体播放列表中单个流的配置文件。 |
| PTMediaSelectionOption | 表示音像媒体资源，以适应不同的语言首选项、辅助功能要求或自定义应用程序配置。 有效的选项类型：<ul><li>字幕(PTMediaSelectionOptionTypeSubtitle)</li><li>替代音频(PTMediaSelectionOptionTypeAudio)</li><li>隐藏式字幕(PTMediaSelectionOptionTypeCC)</li><li>未定义(PTMediaSelectionOptionTypeUndefined)</li></ul> |
| PTOpportunityResolver类，PTOportunityResolver协议 | 用于处理清单内提示的类，这些提示将用作Adobe Primetime广告决策过程的位置。 |
| PTOpportunityResolverDelegate | 描述自定义业务机会解析程序(PTOportunityResolver)用来向委派业务机会解析状态的方法的协议。 |
| PTSDK | 介绍TVSDK的版本及其功能。 |
| PTSDKConfig | 公开TVSDK全局设置并允许应用程序订阅自定义HLS标记。 |
| PTTextStyleRule | 定义表示构成规则字典的文本样式属性键的常量。 |
