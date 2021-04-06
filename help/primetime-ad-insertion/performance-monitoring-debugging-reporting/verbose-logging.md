---
title: 详细记录
description: 详细记录
copied-description: true
exl-id: f2d1b0c2-ba28-4fba-9a4e-71d1421f37fe
translation-type: tm+mt
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '2157'
ht-degree: 0%

---

# 详细日志记录{#verbose-logging}

## ptdebug/logging事件说明{#ptdebug-logging-events}

在为清单服务器会话启动调试日志记录时，可以将`ptdebug`参数添加到请求URL，以指定清单服务器在HTTP头中返回的信息的以下选项：

* `ptdebug=true`
除TRACE_HTTP_HEADER和来自TRACE_AD_CALL记录的大多数调用/响应数据之外的所有记录。

* `ptdebug=AdCall`
仅TRACE_AD_类型(例如TRACE_AD_CALL)记录。

* `ptdebug=Header`
仅TRACE_HTTP_HEADER记录。

## 日志记录的格式{#log-record-formats}

每个日志记录都有一个类型和一组字段，其中有些字段可能是可选的。 直到记录类型的所有记录的字段都相同。 它们提供有关会话的时间戳和信息。 记录类型标识所记录的事件类型，后续字段提供有关所记录事件的信息。

日志记录的结构如下：

`datetime request_id session_id zone_id record_type other fields`.

| 字段 | 类型 | 说明 |
|---|---|---|
| date | 字符串 | 时间戳 |
| request_id | 字符串 | 清单服务器使用的请求ID（Unix时间戳） |
| session_id | 字符串 | 清单服务器使用的会话ID |
| zone_id | 整数 | 区 |
| record_type | 字符串 | 正在记录的事件类型 |
| 其他字段 | vers | 取决于事件类型 |

此类型的记录记录HTTP请求的结果。 `TRACE_REQUEST_INFO`以外的字段按表中显示的顺序显示，以制表符分隔。

| 字段 | 类型 | 说明 |
|---|---|---|
| 状态 | 字符串 | 返回的HTTP状态代码 |
| request_method | 字符串 | HTTP方法(GET或POST) |
| request_uri | 字符串 | HTTP请求URI（无主机） |
| request_length | 整数 | 请求长度（字节） |
| response_length | 整数 | 响应长度（字节） |
| δ | 整数 | 处理请求的时间（毫秒） |
| module_type | 字符串 | 变体、流或VOD |
| remote_address_aud_client_ip | 字符串 | **‡** |
| remote_address_x_fwd_for_hdr_key | 字符串 | **‡** |
| remote_host_port | 字符串 | **‡** |

**‡最** 后三个字段是可选的。

**示例**

```shell
1427263800524 6495aafc-3f34-4047-ad36-350d4f056eb4 189938TRACE_REQUEST_INFO 301 GET /auditude/variant/pubAsset/aHR0cDov. . ..m3u8?u=cecebae72a919de350b9ac52602623f3&z=189938&ptcueformat=turner& sid =yk-cnnlive-003 &ptdebug=true 0 0 0 Variant 111.22.3.44 111.22.3.45 127.0.0.1:46383
```

### TRACE_HTTP_HEADER记录{#trace-http-header-records}

在清单服务器与客户端、广告服务器或内容服务器之间的HTTP调用期间交换的此类记录记录日志HTTP头。 超出TRACE_HTTP_HEADER的字段按表中显示的顺序显示，以制表符分隔。

| 字段 | 类型 | 说明 |
|---|---|---|
| request_type | 字符串 | 请求类型（MAIN或UNKNOWN） |
| request_response | 字符串 | 响应标头（请求或响应） |
| header_name | 字符串 | HTTP头名称 |
| header_value | 字符串 | Base64编码的HTTP头值 |

>[!NOTE]
>
>`request_type`和`header_value`字段为可选字段。

**示例**

```shell
2015-03-25T06:10:00.927Z 1427263800573 6495aa. . . 189938 TRACE_MISC Requesting: /cnn/tvecnn/stream4/stream_Layer.m3u8
2015-03-25T06:10:00.927Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN REQUEST Cookie aGRu. . .
2015-03-25T06:10:00.928Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN REQUEST User-Agent TW96aW. . .
2015-03-25T06:10:01.063Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Server bmd4X2. . .
2015-03-25T06:10:01.063Z  1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Content-Type YXBwb. . .
2015-03-25T06:10:01.063Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Last-Modified V2VkL. . .
2015-03-25T06:10:01.063Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE ETag IjIyY2. . .
2015-03-25T06:10:01.063Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Vary QWNjZXB. . .
2015-03-25T06:10:01.063Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Cache-Control bWF4LW. . .
2015-03-25T06:10:01.064Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Expires V2VkL. . .
2015-03-25T06:10:01.064Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Date V2VkLCA. . .
2015-03-25T06:10:01.064Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Age MQ==
2015-03-25T06:10:01.064Z 1427263800573 6495aa. . . 189938 TRACE_HTTP_HEADER UNKNOWN RESPONSE Via MS4xIH. . .
```

### TRACE_AD_CALL记录{#tracing-ad-call-records}

此类型的记录记录清单服务器和请求的结果。 `TRACE_AD_CALL`以外的字段按表中显示的顺序显示，以制表符分隔。

| 字段 | 类型 | 说明 |
|---|---|---|
| 状态 | 字符串 | 返回的HTTP状态代码 |
| request_duration | 整数 | 请求到响应的时间（毫秒） |
| ad_server_查询_url | 字符串 | 广告调用的URL，包括查询参数 |
| ad_system_id | 字符串 | 广告系统，从广告服务器响应（如果未指定，则为Auditude） |
| avail_id | 字符串 | 可用的ID，来自内容清单文件（VOD为N/A）中的ad提示 |
| avail_duration | number | 可用的持续时间（秒），从内容清单文件中的广告提示（VOD为N/A） |
| ad_server_response | 字符串 | 来自广告服务器的Base64编码响应 |

示例：

```shell
2015-03-25T06:13:31.271Z 14272. . . 189938 TRACE_AD_CALL200 8 https://ad.stg2.auditude.com/adserver/a?cip=0.0.0.0&g=1000012&of=1.5 &ptcueformat=turner&ptdebug=true&tl=l,150,30,m&tm=63&u=ceceb. . . Auditude IvpIyC. . . 150 PD94bWw. . .
```

### TRACE_AD_INSERT、TRACE_AD_RESOLVE和TRACE_AD_REDIRECT记录{#trace-ad-insert-resolve-redirect}

此类型的记录记录记录类型指示的广告请求的结果。 记录类型以外的字段按表中显示的顺序显示，以制表符分隔。

| 字段 | 类型 | 说明 |
|---|---|---|
| 状态 | 字符串 | 返回HTTP状态代码。 |
| avail_id | 字符串 | 可用的ID，从内容清单文件（实时）中的ad提示或从清单服务器(VOD)。 |
| ad_type | 字符串 | 广告类型（直接或重定向）。 |
| ad_duration | 整数 | 广告的持续时间（秒），来自广告服务器响应。 |
| ad_content_url | 字符串 | 广告的清单文件的URL，来自广告服务器响应。 |
| **†** ad_content_url_actual | 字符串 | 插入广告的清单文件的URL。 对于TRACE_AD_REDIRECT为空。 |
| ad_system_id | 字符串 | 广告系统，从广告服务器响应（如果未指定，则为Auditude）。 |
| ad_id | 字符串 | 广告的ID，来自广告服务器响应。 |
| creative_id | 字符串 | 创意的ID，从广告节点，从广告服务器响应。 |
| **†** ad_call_id | 字符串 | 未使用。 保留供将来使用。 |
| δ | 整数 | 此事件所花费的时间（毫秒）。 |
| **†杂** 项 | 字符串 | 已跳过原因广告。 |

**†、** `ad_content_url_actual`和 `ad_call_id`字段 `misc` 是可选的。

>[!NOTE]
>
>对于`TRACE_AD_RESOLVE`和`TRACE_AD_INSERT`,`ad_content_url_actual`字段中的URL用于转码广告（如果有）。 否则，`TRACE_AD_RESOLVE`的字段为空，或与`TRACE_AD_INSERT`的`ad_content_url`相同。

示例：

```shell
2015-03-18T22:25:36.229-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_RESOLVE200 0 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 Auditude 308008 0  cecebae72a919de350b9ac52602623f3 0 NA
2015-03-18T22:25:36.230-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_RESOLVE200 2 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 Auditude 308008 0  cecebae72a919de350b9ac52602623f3 0 NA
2015-03-18T22:25:36.562-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_INSERT200 0 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8Auditude 308008 0 cecebae72a919de350b9ac52602623f3 0 NA
2015-03-18T22:25:36.563-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_INSERT200 2 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8Auditude 308008 0 cecebae72a919de350b9ac52602623f3 0 NA
```

<!-- ### TRACE_TRACKING_URL records {#trace-tracking-url-records}

Records of this type log the results of manifest server ad requests. Fields beyond `TRACE_TRACKING_URL` appear in the order shown in the table, separated by tabs.

| Field | Type | Description |
|---|---|---|
| pts | number | Program timestamp. Time within video to call the URL. |
| ad_system | string | Ad system (auditude or freewheel) |
| url | string | URL pinged |
| status | string | HTTP status returned from the ping |

```shell
2015-06-04T23:24:42.000-0700 1426742736208 3086f5cd . . . 12345 TRACE_TRACKING_URL 0.000000 ExampleSystem https://localhost/index.php?stream:test#8.1433485415; sid:3086f5cd . . .;pts:0 200
```

-->

### TRACE_TRANSCODE_NO_MEDIA_TO_TRANSCODE记录{#trace-transcoding-no-media-to-transcode}

此类型的记录记录缺少广告创意。 表中出现唯一超出`TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE`的字段。

| 字段 | 类型 | 说明 |
|---|---|---|
| ad_id | 字符串 | 完全限定的广告ID(FQ_AD_ID:Q_AD_ID\[;Q_AD_ID\[;Q_AD_ID...\] \] Q_AD_ID:协议：AD_SYSTEM:AD_ID\[:CREATIVE_ID\[:MEDIA_ID\] \]协议：AUDITUDE， VAST) |

此类型的记录记录清单服务器发送给CRS的转码请求的结果。 `TRACE_TRANSCODING_REQUESTED`以外的字段按表中显示的顺序显示，以制表符分隔。

| 字段 | 类型 | 说明 |
|---|---|---|
| ad_id | 字符串 | 完全限定的广告ID |
| ad_manifest_url | 字符串 | 广告的清单文件的URL，来自广告服务器响应 |
| creative_type | 字符串 | 媒体类型 |
| 标志 | 字符串 | ID3指示转码请求是否包括添加ID3标记的请求 |
| 目标_duration | 字符串 | 转码创意的目标持续时间（秒） |

此类型的记录指示执行服务器端跟踪的请求。 `TRACE_TRACKING_REQUEST`以外的字段按表中显示的顺序显示，以制表符分隔。

| 字段 | 类型 | 说明 |
|---|---|---|
| tracking_url_count | 整数 | 跟踪URL的数量 |
| 开始 | 浮 | PTS片段开始时间（秒，精确到毫秒） |
| 结束 | 浮 | PTS片段结束时间（秒，精确到毫秒） |

此类型的记录为服务器端跟踪提供跟踪URL。 `TRACE_TRACKING_REQUEST_URL`以外的字段按表中显示的顺序显示，以制表符分隔。

| 字段 | 类型 | 说明 |
|---|---|---|
| 时间戳 | 浮 | 播放会话中ping跟踪URL的时间（秒，精度为。001）。 |
| ad_system | 字符串 | 广告系统（例如，auditude） |
| url | 字符串 | 要ping的URL |

清单服务器为`WEBVTT`题注发出此类型日志记录请求。 `TRACE_WEBVTT_REQUEST`以外的字段按表中显示的顺序显示，以制表符分隔。

| 字段 | 类型 | 说明 |
|---|---|---|
| 状态 | 字符串 | 返回的HTTP状态代码 |
| vtt_uri | 字符串 | 请求的URL |
| 开始 | 浮 | 分割开始时间（秒，毫秒精度） |
| 结束 | 浮 | 分段结束时间（秒，精确到毫秒） |

清单服务器向`answer`中的客户端发送的此类型日志记录响应对`WEBVTT`字幕的请求。 `TRACE_WEBVTT_RESPONSE`以外的字段按表中显示的顺序显示，以制表符分隔。

| 字段 | 类型 | 说明 |
|---|---|---|
| 状态 | 字符串 | 返回的HTTP状态代码 |
| 响应 | 字符串 | 发送到客户端的Base64编码响应 |

清单服务器对请求做出的此类记录日志响应用于`WEBVTT`题注。 `TRACE_WEBVTT_SOURCE`以外的字段按表中显示的顺序显示，以制表符分隔。

| 字段 | 类型 | 说明 |
|---|---|---|
| 状态 | 字符串 | 返回的HTTP状态代码 |
| 源 | 字符串 | 基于64编码的原始VTT内容 |

此类型的记录使清单服务器能够记录事件和在收录广告时未计划的信息。 `TRACE_MISC`之外的字段由消息字符串组成。 可能显示的消息包括：

* 广告被忽略：AdPlacement \[adManifestURL=https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb。...m3u8, durationSeconds=15.0,ignore=false， redirectAd=false， priority=1\]
* AdPlacement adManifestURL= adManifestURL， durationSeconds= seconds， ignore= ignore， redirectAd= redirectAd， priority= priority
* 广告投放返回null。
* 已成功拼接广告。
* 广告呼叫失败：错误消息。
* 添加User-Agent以获取原始清单：用户代理。
* 添加Cookie以获取原始清单：#
* 错误的URL请求的URL错误消息。 （无法分析变体URL）
* 调用的url:URL获得回车：响应代码。 （实时URL）
* 调用的url:URL返回代码：响应代码。 (VOD URL)
* 解决广告时发现冲突：中间辊开始或中间辊端之一位于中间辊(VOD)中包含的预辊或预辊内。
* 检测到处理函数为URI引发的未处理异常：请求URL。
* 已完成生成变型清单。 （变量）
* 已完成生成变型清单。
* 处理VAST重定向*重定向URL时出现异常*错误：错误消息。
* 无法获取广告清单URL的播放列表。
* 无法生成目标清单。 (HLSManifestResolver)
* 无法分析第一个广告调用响应：错误消息。
* 无法处理*GET|POST*路径请求：请求URL。 （实时/VOD）
* 无法处理Live Manifest请求：请求URL。 （实时）
* 无法返回变量清单：错误消息。
* 无法验证组ID:组ID。
* 正在获取原始清单：内容URL。 （实时）
* 在VAST重定向后：重定向URL。
* 找到空的可用。 (VOD)
* 找到&#x200B;*数字*&#x200B;广告。 (VOD)
* 收到HTTP请求。 （第一条消息）
* 将忽略广告，因为广告响应持续时间（*广告响应持续时间*秒）和实际广告持续时间（*实际持续时间*秒）之间的差异大于限制。 (HLSManifestResolver)
* 将忽略未提供ID值的可用值。 (GroupAdResolver.java)
* 忽略提供无效时间值的有用值：*time *for availId = avail ID。
* 忽略提供无效持续时间值的有用值：*duration *for availId = avail ID。
* 初始化新会话。 （变量）
* HTTP方法无效。 一定是GET。 (VOD)
* HTTP方法无效。 跟踪请求必须是GET。 （实时）
* 请求的URL错误消息无效。 （变量）
* 组无效。 (HLSManifestResolver)
* 请求无效。 题注不是有效的跟踪请求。 (VOD)
* 请求无效。 必须在会话建立后发出题注请求。 (VOD)
* 请求无效。 必须在会话建立后发出跟踪请求。 (VOD)
* 超载组ID的服务器实例无效：组ID。 （实时）
* 已达到VAST重定向的限制 — 数量。
* 进行广告通话：广告呼叫URL。
* 找不到以下对象的清单：内容URL。 （实时）
* 找不到适用ID的匹配用项：可用ID。 (HLSManifestResolver)
* 未找到播放会话。 (HLSManifestResolver)
* 正在处理清单内容URL的VOD请求。
* 正在处理变量。
* 正在处理清单内容URL的题注请求。
* 正在处理跟踪请求。 (VOD)
* 重定向广告响应为空。 (VASTStAX)
* 请求：URL。
* 返回GET请求的错误响应，因为未找到播放会话。 (VOD)
* 因内部服务器错误而返回GET请求的错误响应。
* 为指定无效资产的GET请求返回错误响应：广告请求ID。 (VOD)
* 为指定无效或空组ID的GET请求返回错误响应：组ID。 (VOD)
* 为指定无效跟踪位置值的GET请求返回错误响应。 (VOD)
* 对语法无效的GET请求返回错误响应 — 请求URL。 （实时/VOD）
* 使用不支持的HTTP方法返回请求的错误响应：GET|POST。 （实时/VOD）
* 从缓存返回清单。 (VOD)
* 服务器已过载。 无需广告拼合请求即可继续。 （变量）
* 开始生成目标清单。 (HLSManifestResolver)
* 开始生成变型清单自：内容URL。 （变量）
* 开始将广告拼接到清单中。 (VODHLSResolver)
* 尝试在`HH:MM:SS`处缝合广告：AdPlacement \[adManifestURL= ad Manifest URL， durationSeconds= seconds， ignore= ignore， redirectAd= redirect ad， priority= priority.\] \(HLSManifestResolver\)
* 由于时间轴无效，无法获取广告 — 返回不含广告的内容。 (VOD)
* 无法获取广告 — 返回不含广告的内容。 (VOD)
* 无法获取广告查询，未提供内容URL。 (VOD)
* 收到有效的URL。 (VOD/Variant)
* 找不到变体M3U8。 （变量）

### TRACE_PLAYBACK_PROGRESS记录{#trace-playback-progress-records}

清单服务器在服务器端跟踪工作流期间接收关于播放进度的信号时生成这种记录。 `TRACE_PLAYBACK_PROGRESS`以外的字段按表中显示的顺序显示，以制表符分隔。

| 字段 | 类型 | 说明 |
|---|---|---|
| 状态 | 字符串 | HTTP状态代码 |
| 带宽 | 整数 | 流的带宽 |
| pts | 整数 | 流中的PTS时间 |
| ms_time | 整数 | 清单服务器生成跟踪URL的时间 |
| url | 字符串 | 重定向URL |
| **** header_user_agent | 字符串 | HTTP用户代理头 |
| **** header_dnt | 整数 | HTTP do-not-track头 |
| **** effective_remote_address | 字符串 | IPv4有效远程地址 |
| **** remote_address | 字符串 | IPv4远程地址 |

**最** 后四个字段是可选的。

## 多比特率流{#multiple-bitrate-streams}

客户端广告插入请求通常在变体M3U8格式的播放列表中指定多个比特率。 清单服务器生成并返回一个新的变体M3U8文件，其中每个比特率包含一个单独的M3U8链接。 它还生成一个唯一的组ID来将这些M3U8绑定在一起。

清单服务器使用客户端的BootstrapURL请求中的信息来检索内容变体播放列表。 它生成一个新的变体播放列表，其中包含指向流级内容的清单服务器链接。 客户端使用它们来构建广告插入请求。 清单服务器的流级内容链接具有以下格式：

```shell
https://manifest.auditude.com/auditude/{live/vod}/{publisherAssetID}/{rendition}/
{groupID}/{base64-encoded url of the bit rate stream}.[m3u8]?{Query parameters}
```

* **live/**
vod清单服务器根据内容的播放列表类型设置此值：实时/线性(
`#EXT-X-PLAYLIST-TYPE:EVENT`)或VOD(`#EXT-X-PLAYLIST-TYPE:VOD`)

* **publisherAssetIDPublisher对**
于BootstrapURL请求中提供的特定内容的唯一ID。

* **演**
绎版清单服务器根据 
`BANDWIDTH` 值，并使用它将广告的比特率与内容的比特率相匹配。除非具有最低比特率的广告再现超过内容的比特率，否则广告比特率不能超过内容的比特率。

* **groupIDT**
清单服务器生成此值并使用它来确保它一致地放置广告，而不管客户端请求广告的位速率再现为什么。

* **比特率流的base64编码的url清**
单服务器URL安全的base64对内容流的绝对URL进行编码。每个流都有其自己的URL。

* **查询**
参数BootstrapURL请求中提供的查询参数。
