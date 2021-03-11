---
description: '此表提供了有关收入优化通知的详细信息。 '
title: 收入优化代码
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---


# 收入优化代码{#revenue-optimization-code}

此表提供有关收入优化通知的详细信息。

## 启用收入优化报告{#enable-revenue-optimization-reporting}

要启用此报告，请使用PTMediaPlayer api:`[mediaPlayersetRevenueOptimizationReportingLevel:PTNotificationTypeInfo]`。

>[!NOTE]
>
>大多数信息性通知都包含相关元数据，例如，无法下载的资源的URL。 某些通知包含元数据，用于指定问题是在主视频内容、备用音频内容还是广告中出现。

| 代码 | 名称 | 内部通知 | 元数据键 | 评论 |
|---|---|---|---|---|
| 401001 | REVENUE_OPTIMIZATION_报告 | 无 | 有关基于不同事件的元数据键，请参阅下表。 | 无 |

| 事件详细信息 | ContextMetadata |
|---|---|
| **调用MediaPlayer:** replaceCurrentResource时，在TVSDK中修补CONTENT_RESOURCE_STARTD。 | clientTimestamp、fallbackOnInvalidCreative、showStaticBanners、hasPreroll、事件、adSigningMode、resourceUrl、creativeRepackagingFormat、delayAdLoadingTolerance、zoneID、hasLivePreroll、adRequestTimeout、deadAdAdLoadLoading、resourceLoadtype， creativeRepackagingEnabled， mediaId， clientId |
| **当内容进入准** 备状态并准备好回放时，在TVSDK中CONTENT_PLAYBACK_STARTD已打补丁。此事件不会在每次清单上传时调度 — 只会在初始负载时调度。 | clientTimestamp、contentURL、contentType、事件、isLive、clientID |
| **AD_OPPORTUNITY_GENERATED在生** 成机会时在TVSDK中进行修补。 | clientTimestamp，事件, opportunityId， placementDuration， clientId |
| **AD_OPPORTUNITY_RESOLVE_STARTD在机** 会开始解析时在TVSDK中打补丁。 | clientTimestamp，事件, opportunityId， placementDuration， clientId |
| **AD_OPPORTUNITY_RESOLVE_FAILED在广** 告解析程序调用MediaPlayerClient::notifyFailed()时在TVSDK中打补丁。需要填写数据 | opportunityId， notificationAD |
| **AD_RESOURCE_LOADD在** 通过URL获取任何广告资源时进行修补。responseStartTime：请求首次启动时的Unix时间戳。 responseTotalTime：响应加载所花费的总时间（以秒为单位）。 responseStatus：获取资源时遇到的状态代码。 status:&quot;error&quot;或&quot;success&quot; referrerAdId：请求获取此资源的引用ad id（如果存在）。 referrerUrl：请求获取此资源的引用url。 errorMessage：如果状态为“error”，则此处将找到错误原因。 | opportunityId， resourceType， responseTotalTime， responseStatus， responseStartTime， status， errorMessage， url， referrerURL， referrerAdId |
| **将CRS应用于资** 产时在TVSDK中安装AD_RESOURCE_LOAD_CRSD以及m3u8的响应。resourceType:always &quot;crs&quot;。 responseStartTime：请求首次启动时的Unix时间戳。 responseTotalTime：响应加载所花费的总时间（以秒为单位）。 responseStatus：获取资源时遇到的状态代码。 status:&quot;error&quot;或&quot;success&quot;。 errorMessage：如果状态为“error”，则此处将找到错误原因。 mediaFileUrl：所选的原始媒体文件url。 mediaFileBitrate：所选媒体文件的比特率。 mediaFileMimeType:所选媒体文件的MIME类型。 url：最终的资产url。 | opportunityId， resourceType， responseTotalTime， responseStatus， responseStartTime， status， errorMessage， url， mediaFileURL， mediaFileBitrate， mediaFileMimeType， url |
| **在将adBreak放置到** 时间轴后，TVSDK中的AD_TIMELINE_PLACEDispatched。每个广告中断一次事件。 propededTime：请求放置广告分段的时间。 actualTime：广告分段的实际放置时间。 propededDuration：请求插入的广告分段的持续时间。 对于实时内容，这将是提示持续时间。 对于VOD内容，此值通常为–1。 actualDuration：插入的广告分段的实际持续时间。 计算为在原始流时间轴中添加或替换的所有广告的总持续时间，由其各自的区段持续时间定义。 positedAds：建议广告中的广告数。 totalAds：成功投放的广告数。 广告……n：成功插入广告将插入此处。 可以从AD_OPPORTUNITY_RESOLVE_PROCESS检索整个广告清单信息 | opportunityId， status， errorMessage， proposedTime， proposedDuration， actualTime， actualDuration， proposedAds， totalAds， ads_id， ads_type， ads_duration， ads_url |
| **在广告开始播** 放后在TVSDK中修补AD_PLAYBACK_STARTD。 | clientTimestamp，事件, id， url，持续时间， type， opportunityId， clientId |
| **AD_PLAYBACK_COMPLETED在广** 告完成播放后在TVSDK中进行修补。 | clientTimestamp，事件, id， url，持续时间， type， opportunityId， clientId |
| **ADBREAK_PLAYBACK_STARTD在** adbreak开始播放时在TVSDK中打补丁。 | clientTimestamp，事件, opportunityId，持续时间， time， clientId |
| **当adbreak完成播放** 时，ADBREAK_PLAYBACK_COMPLETED在TVSDK中打补丁。 | clientTimestamp，事件, opportunityId， clientId |
| **CONTENT_PLAYBACK_COMPLETED在任** 何内容完成时在TVSDK中进行修补。如果替换流、播放器进入错误状态、播放器被重置或内容实际完成，则可能会发生这种情况。必须使用此事件来跟踪sessionId。 | clientTimestamp，事件, clientId， url， status， errorMessage |
| **AD_PLAYBACK_ERRORD在广** 告回放时出错（变型流错误）时在TVSDK中打补丁。 | 事件、错误、时间戳、manifestUrl、time、opportunityId、url |
