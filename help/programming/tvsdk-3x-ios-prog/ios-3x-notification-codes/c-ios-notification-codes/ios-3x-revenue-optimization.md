---
description: 此表提供有关收入优化通知的详细信息。
title: 收入优化代码
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---

# 收入优化代码 {#revenue-optimization-code}

此表提供有关REVENUE OPTIMIZATION通知的详细信息。

## 启用收入优化报表 {#enable-revenue-optimization-reporting}

要启用此报表，请使用PTMediaPlayer API： `[mediaPlayersetRevenueOptimizationReportingLevel:PTNotificationTypeInfo]`.

>[!NOTE]
>
>大多数信息性通知包含相关元数据，例如，下载失败的资源的URL。 某些通知包含元数据，用于指定问题出现在主视频内容、备用音频内容还是广告中。

| 代码 | 名称 | 内部通知 | 元数据键 | 评论 |
|---|---|---|---|---|
| 401001 | REVENUE_OPTIMIZATION_REPORTING | 无 | 有关基于不同事件的元数据键，请参阅下表。 | 无 |

| 活动详细信息 | 上下文元数据 |
|---|---|
| **CONTENT_RESOURCE_START** 在调用MediaPlayer：：replaceCurrentResource时在TVSDK中调度。 | clientTimestamp， fallbackOnInvalidCreative， showStaticBanners， hasPreroll， event， adSignalingMode， resourceUrl， creativeRepackagingFormat， delayAdLoadingTolerance， zoneID， hasLivePreroll， adRequestTimeout， delayAdLoading， resourceType， creativeRepackagingEnabled， mediaId， cliventId |
| **CONTENT_PLAYBACK_START** 当内容已进入准备状态并准备好播放时，在TVSDK中调度。 此事件不会在每次清单上传时调度 — 仅在初始加载时调度。 | clientTimestamp， contentURL， contentType， event， isLive， clientID |
| **AD_OPPORTUNITY_GENERATED** 在生成机会时在TVSDK中调度。 | clientTimestamp、event、opportunityId、placementDuration、clientId |
| **AD_OPPORTUNITY_RESOLVE_START** 当机会开始解析时在TVSDK中调度。 | clientTimestamp、event、opportunityId、placementDuration、clientId |
| **AD_OPPORTUNITY_RESOLVE_FAILED** 当广告解析程序调用MediaPlayerClient：：notifyFailed()时，在TVSDK中调度。 需要填写数据 | opportunityId， notificationAD |
| **AD_RESOURCE_LOAD** 通过URL获取任何广告资源时调度。 responseStartTime：请求首次启动时间的Unix时间戳。 responseTotalTime：加载响应所花费的总时间（以秒为单位）。 responseStatus：获取资源时遇到的状态代码。 status：&quot;error&quot;或&quot;success&quot; referrerAdId：请求提取此资源的反向链接广告ID（如果存在）。 referrerUrl：请求获取此资源的反向链接URL。 errorMessage：如果状态为“error”，错误原因将位于此处。 | opportunityId， resourceType， responseTotalTime， responseStatus， responseStartTime， status， errorMessage， url， referrerURL， referrerAdId |
| **AD_RESOURCE_LOAD_CRS** 将CRS应用于资产以及m3u8的响应时，在TVSDK中分发。 resourceType：始终为“crs”。 responseStartTime：请求首次启动时间的Unix时间戳。 responseTotalTime：加载响应所花费的总时间（以秒为单位）。 responseStatus：获取资源时遇到的状态代码。 状态：“错误”或“成功”。 errorMessage：如果状态为“error”，错误原因将位于此处。 mediaFileUrl：所选的原始媒体文件URL。 mediaFileBitrate：所选媒体文件的比特率。 mediaFileMimeType：所选媒体文件的mime类型。 url：最终资源url。 | opportunityId， resourceType， responseTotalTime， responseStatus， responseStartTime， status， errorMessage， url， mediaFileURL， mediaFileBitrate， mediaFileMimeType， url |
| **AD_TIMELINE_PLACE** 在时间线上放置一个adBreak后，在TVSDK中调度。 此事件将在每个广告时间发生一次。 proposedTime：请求放置广告时间的时间。 actualTime：广告时间实际放置的时间。 proposedDuration：请求插入的广告时间的持续时间。 对于实时内容，这将是提示持续时间。 对于VOD内容，该值通常为–1。 actualDuration：插入的广告时间的实际持续时间。 计算为在原始流时间轴中添加或替换的所有广告的总持续时间，由其各自的区段持续时间定义。 proposedAds：建议的广告时间中的广告数。 totalAds：成功投放的广告数。 广告……n：成功插入的广告将插入此处。 可以从AD_OPPORTUNITY_RESOLVE_PROCESS中检索整个广告清单信息 | opportunityId、status、errorMessage、proposedTime、proposedDuration、actualTime、actualDuration、proposedAds、totalAds、ads_id、ads_type、ads_duration、ads_url |
| **AD_PLAYBACK_START** 在广告开始播放后在TVSDK中调度。 | clientTimestamp，事件， id， url，持续时间，类型， opportunityId， clientId |
| **AD_PLAYBACK_COMPLETE** 在广告完成播放后在TVSDK中调度。 | clientTimestamp，事件， id， url，持续时间，类型， opportunityId， clientId |
| **ADBREAK_PLAYBACK_START** 当adbreak开始播放时在TVSDK中调度。 | clientTimestamp， event， opportunityId， duration， time， clientId |
| **ADBREAK_PLAYBACK_COMPLETE** 在广告时间完成播放时在TVSDK中调度。 | clientTimestamp、event、opportunityId、clientId |
| **CONTENT_PLAYBACK_COMPLETE** 完成任何内容时在TVSDK中分发。如果流被替换、播放器进入错误状态、播放器被重置或内容实际完成，则可能会发生这种情况。 跟踪sessionId需要此事件。 | clientTimestamp，事件， clientId， url，状态， errorMessage |
| **AD_PLAYBACK_ERROR** 当广告发生播放错误（变量流错误）时，在TVSDK中调度。 | 事件，错误，时间戳， manifestUrl，时间， opportunityId， url |
