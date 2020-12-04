---
description: '此表提供了有关收入优化通知的详细信息。 '
seo-description: '此表提供了有关收入优化通知的详细信息。 '
seo-title: 收入优化代码
title: 收入优化代码
translation-type: tm+mt
source-git-commit: df3d60874701383325be1afdd1ec5fe036f855f8
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 0%

---


# 收入优化代码{#revenue-optimization-code}

此表提供有关收入优化通知的详细信息。

## 启用收入优化报告{#enable-revenue-optimization-reporting}

要启用此报告，请使用PTMediaPlayer api:`[mediaPlayersetRevenueOptimizationReportingLevel:PTNotificationTypeInfo]`。

>[!NOTE]
>
>大多数信息性通知都包含相关元数据，例如，无法下载的资源URL。 某些通知包含元数据，用于指定在主视频内容、备用音频内容还是广告中出现问题。

| 代码 | 名称 | 内部通知 | 元数据键 | 注释 |
|---|---|---|---|---|
| 401001 | REVENUE_OPTIMIZATION_报告 | 无 | 有关基于不同事件的元数据键，请参阅下表。 | 无 |

| 事件详细信息 | ContextMetadata |
|---|---|
| **调用MediaPlayer:** replaceCurrentResource时，TVSDK中已修补CONTENT_RESOURCE_STARTD。 | clientTimestamp、fallbackOnInvalidCreative、showStaticBanners、hasPreroll、事件、adSignalingMode、resourceUrl、creativeRepackagingFormat、delayAdLoadingTolerance、zoneID、hasLivePrel、adTimeout、deadAdLoading、resourceAdMetype, creativeRepackagingEnabled, mediaId, clientId |
| **当内容进入** 准备状态并准备好回放时，CONTENT_PLAYBACK_STARTD在TVSDK中打补丁。此事件不会在每次清单上传时调度——只会在初始负载时调度。 | clientTimestamp、contentURL、contentType、事件、isLive、clientID |
| **在生成业务机** 会时，AD_OPPORTUNITY_GENERATED在TVSDK中进行修补。 | clientTimestamp,事件, opportunityId, placementDuration, clientId |
| **AD_OPPORTUNITY_RESOLVE_STARTD在机** 会开始解析时在TVSDK中打补丁。 | clientTimestamp,事件, opportunityId, placementDuration, clientId |
| **AD_OPPORTUNITY_RESOLVE_FAILED在广** 告解析程序调用MediaPlayerClient::notifyFailed()时在TVSDK中修补。需要填写数据 | opportunityId, notificationAD |
| **AD_RESOURCE_LOADD** 在通过URL获取任何广告资源时进行修补。responseStartTime：请求首次启动时的Unix时间戳。 responseTotalTime：响应加载所花费的总时间（以秒为单位）。 responseStatus：获取资源时遇到的状态代码。 status:&quot;error&quot;或&quot;success&quot; referrerAdId：请求获取此资源的引用ad id（如果存在）。 referrerUrl：请求获取此资源的引用url。 errorMessage：如果状态为“error”，则错误原因将在此处找到。 | opportunityId, resourceType, responseTotalTime, responseStatus, responseStartTime, status, errorMessage, url, referrerURL, referrerAdId |
| **将CRS应用于资** 产时在TVSDK中修补AD_RESOURCE_LOAD_CRSD以及m3u8的响应。resourceType:always &quot;crs&quot;。 responseStartTime：请求首次启动时的Unix时间戳。 responseTotalTime：响应加载所花费的总时间（以秒为单位）。 responseStatus：获取资源时遇到的状态代码。 status:&quot;error&quot;或&quot;success&quot;。 errorMessage：如果状态为“error”，则错误原因将在此处找到。 mediaFileUrl：已选择的原始媒体文件url。 mediaFileBitrate：所选媒体文件的比特率。 mediaFileMimeType:所选媒体文件的mime类型。 url：最终资产url。 | opportunityId, resourceType, responseTotalTime, responseStatus, responseStartTime, status, errorMessage, url, mediaFileURL, mediaFileBitrate, mediaFileMimeType, url |
| **在将adBreak放** 置到时间轴后，TVSDK中的AD_TIMELINE_PLACED已修补。每个广告中断将发生一次此事件。 portisedTime：请求放置广告中断的时间。 actualTime：广告中断的实际放置时间。 proposedDuration：请求插入的广告分段的持续时间。 对于实时内容，这将是提示持续时间。 对于VOD内容，此值通常为-1。 actualDuration：插入广告分段的实际持续时间。 计算为在原始流时间线中添加或替换的所有广告的总持续时间（由其各自的段持续时间定义）。 portisedAds：建议广告分段中的广告数。 totalAds：成功投放的广告数。 广告……n：此处将插入成功插入广告。 可从AD_OPPORTUNITY_RESOLVE_PROCESS检索整个广告清单信息 | opportunityId, status, errorMessage, proposedTime, pospotedDuration, actualTime, actualDuration, posportentAds, totalAds, adsid, ads_type, ads_duration, ads_url |
| **在广告开始播** 放后在TVSDK中修补AD_PLAYBACK_STARTD。 | clientTimestamp,事件, id, url，持续时间，类型， opportunityId, clientId |
| **AD_PLAYBACK_COMPLETED在** 广告完成播放后在TVSDK中进行修补。 | clientTimestamp,事件, id, url，持续时间，类型， opportunityId, clientId |
| **ADBREAK_PLAYBACK_STARTD在** TVSDK中进行修补，当adbreak开始播放时。 | clientTimestamp,事件, opportunityId，持续时间，时间，clientId |
| **当adbreak完成播放** 时，ADBREAK_PLAYBACK_COMPLETED在TVSDK中打补丁。 | clientTimestamp,事件, opportunityId, clientId |
| **当任何内容** 完成时，TVSDK中都安装了CONTENT_PLAYBACK_COMPLETED。如果替换流、播放器进入错误状态、播放器被重置或内容实际完成，则可能会发生这种情况。必须使用此事件来跟踪sessionId。 | clientTimestamp,事件, clientId, url, status, errorMessage |
| **当广告回** 放时出错（变型流错误）时，AD_PLAYBACK_ERRORD在TVSDK中打补丁。 | 事件、错误、时间戳、manifestUrl、time、opportunityId、url |
