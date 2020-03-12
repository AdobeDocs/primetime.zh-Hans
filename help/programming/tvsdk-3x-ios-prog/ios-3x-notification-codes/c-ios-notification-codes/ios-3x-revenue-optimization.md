---
description: '此表提供有关收入优化通知的详细信息。 '
seo-description: '此表提供有关收入优化通知的详细信息。 '
seo-title: 收入优化代码
title: 收入优化代码
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 收入优化代码 {#revenue-optimization-code}

此表提供有关收入优化通知的详细信息。

## 启用收入优化报告 {#enable-revenue-optimization-reporting}

要启用此报告，请使用PTMediaPlayer api: `[mediaPlayer
setRevenueOptimizationReportingLevel:PTNotificationTypeInfo]`.

[!N注意]:大多数信息性通知都包含相关元数据，例如，无法下载的资源的URL。 某些通知包含元数据，用于指定问题是在主视频内容、备用音频内容中还是在广告中发生。

|代码|名称|内部通知|元数据键|注释||—|—|—|—|| 401001| REVENUE_OPTIMIZATION_REPORTING|无|有关基于不同事件的元数据键，请参阅下表。 |无|

| 活动详细信息 | ContextMetadata |
|---|---|
| **CONTENT_RESOURCE_START** 在调用MediaPlayer::replaceCurrentResource时在TVSDK中调度。 | clientTimestamp, fallbackOnInvalidCreative, showStaticBanners, hasPreroll, event, adSignalingMode, resourceUrl, creativeRepackagingFormat, delayAdLoadingTolerance, zoneID, hasLivePreloverl, adRequestTimeout, adAdAdAdAdAdDemownet, resource, deypet, resource, resource, resourceAdType, resourceRemons, resourceRead, resource, resourceReadRew, creativeRepackagingEnabled, mediaId, clientId |
| **CONTENT_PLAYBACK_START** 当内容已进入准备状态并准备好回放时在TVSDK中调度。 此事件不会在每次清单上传时调度——只会在初始加载时调度。 | clientTimestamp、contentURL、contentType、event、isLive、clientID |
| **AD_OPPORTUNITY_GENERATED** 在生成业务机会时在TVSDK中调度。 | clientTimestamp，事件， opportunityId, placementDuration, clientId |
| **AD_OPPORTUNITY_RESOLVE_START** 当业务机会开始解析时在TVSDK中调度。 | clientTimestamp，事件， opportunityId, placementDuration, clientId |
| **AD_OPPORTUNITY_RESOLVE_FAILED** 当广告解析程序调用MediaPlayerClient::notifyFailed()时在TVSDK中调度。 需要填写数据 | opportunityId, notificationAD |
| **AD_RESOURCE_LOAD** 当通过URL获取任何广告资源时调度。 responseStartTime：请求首次启动时的Unix时间戳。 responseTotalTime：响应加载所用的总时间（以秒为单位）。 responseStatus：获取资源时遇到的状态代码。 status:&quot;error&quot; or &quot;success&quot; referrerAdId：请求获取此资源的引用广告ID（如果有）。 referrerUrl：请求获取此资源的引用URL。 errorMessage：如果状态为“error”，则此处将找到错误原因。 | opportunityId, resourceType, responseTotalTime, responseStatus, responseStartTime, status, errorMessage, url, referrerURL, referrerAdId |
| **AD_RESOURCE_LOAD_CRS** 在将CRS应用于资产以及m3u8的响应时在TVSDK中调度。 resourceType:always &quot;crs&quot;。 responseStartTime：请求首次启动时的Unix时间戳。 responseTotalTime：响应加载所用的总时间（以秒为单位）。 responseStatus：获取资源时遇到的状态代码。 status:&quot;error&quot;或&quot;success&quot;。 errorMessage：如果状态为“error”，则此处将找到错误原因。 mediaFileUrl：选定的原始媒体文件url。 mediaFileBitrate：所选媒体文件的比特率。 mediaFileMimeType:所选媒体文件的mime类型。 url：最终资产URL。 | opportunityId, resourceType, responseTotalTime, responseStatus, responseStartTime, status, errorMessage, url, mediaFileURL, mediaFileBitrate, mediaFileMimeType, url |
| **在将adBreak放置到时间轴后，在TVSDK中调度AD_TIMELINE_PLACE** 。 每个广告中断将发生一次此事件。 powsedTime：请求投放广告的时间。 actualTime：广告中断的实际放置时间。 propedDuration：请求插入的广告分时段的持续时间。 对于实时内容，这将是提示持续时间。 对于VOD内容，此值通常为-1。 actualDuration：插入的广告中断的实际持续时间。 计算为在原始流时间线中添加或替换的所有广告的总持续时间（由其各自的段持续时间定义）。 propedAds：建议广告分时段中的广告数。 totalAds：成功投放的广告数。 广告……n：成功插入广告将插入此处。 可从AD_OPPORTUNITY_RESOLVE_PROCESS检索整个广告清单信息 | opportunityId, status, errorMessage, porposedTime, proposedDuration, actualTime, actualDuration, porposedAds,totalAds, ads_id, ads_type, ads_duration, ads_url |
| **AD_PLAYBACK_START** 在广告开始播放后在TVSDK中调度。 | clientTimestamp，事件， id, url，持续时间，类型， opportunityId, clientId |
| **AD_PLAYBACK_COMPLETE** 在广告完成播放后在TVSDK中调度。 | clientTimestamp，事件， id, url，持续时间，类型， opportunityId, clientId |
| **ADBREAK_PLAYBACK_START** 在adbreak开始播放时在TVSDK中调度。 | clientTimestamp，事件， opportunityId，持续时间，时间， clientId |
| **ADBREAK_PLAYBACK_COMPLETE** 当adbreak完成播放时在TVSDK中调度。 | clientTimestamp, event, opportunityId, clientId |
| **CONTENT_PLAYBACK_COMPLETE** 当任何内容完成时在TVSDK中调度。如果替换流、播放器进入错误状态、播放器重置或内容实际完成，则可能会发生这种情况。 跟踪sessionId时需要此事件。 | clientTimestamp，事件， clientId, url, status, errorMessage |
| **AD_PLAYBACK_ERROR** 当广告回放错误（变体流错误）时在TVSDK中调度。 | event, error, timestamp, manifestUrl, time, opportunityId, url |