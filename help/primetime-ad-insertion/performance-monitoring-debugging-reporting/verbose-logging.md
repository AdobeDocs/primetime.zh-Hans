---
title: 详细日志记录
description: 详细日志记录
copied-description: true
exl-id: f2d1b0c2-ba28-4fba-9a4e-71d1421f37fe
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '2155'
ht-degree: 0%

---

# 详细日志记录 {#verbose-logging}

## ptdebug/logging事件说明 {#ptdebug-logging-events}

为清单服务器会话启动调试日志记录时，可以添加 `ptdebug` 请求URL的参数，以便为清单服务器在HTTP标头中返回的信息指定以下选项：

* `ptdebug=true`
除TRACE_HTTP_HEADER和大多数调用/响应数据之外的所有记录均来自TRACE_AD_CALL记录。

* `ptdebug=AdCall`
仅TRACE_AD_类型(例如，TRACE_AD_CALL)记录。

* `ptdebug=Header`
仅TRACE_HTTP_HEADER记录。

## 日志记录的格式 {#log-record-formats}

每个日志记录都有一个类型和一组字段，其中一些字段可能是可选的。 记录类型之前的所有记录的字段是相同的。 它们提供时间戳和有关会话的信息。 记录类型标识所记录的事件类型，后续字段提供有关所记录事件的信息。

日志记录的结构如下：

`datetime request_id session_id zone_id record_type other fields`.

| 字段 | 类型 | 描述 |
|---|---|---|
| datetime | 字符串 | 时间戳 |
| request_id | 字符串 | 清单服务器使用的请求ID（Unix时间戳） |
| session_id | 字符串 | 清单服务器使用的会话ID |
| zone_id | 整数 | 区域 |
| record_type | 字符串 | 所记录的事件类型 |
| 其他字段 | 不尽相同 | 取决于事件类型 |

此类型的记录记录HTTP请求的结果。 字段超出 `TRACE_REQUEST_INFO` 按表中显示的顺序显示，用制表符分隔。

| 字段 | 类型 | 描述 |
|---|---|---|
| 状态 | 字符串 | 返回的HTTP状态代码 |
| request_method | 字符串 | HTTP方法(GET或POST) |
| request_uri | 字符串 | HTTP请求URI（不带主机） |
| request_length | 整数 | 请求长度（字节） |
| response_length | 整数 | 响应长度（字节） |
| delta | 整数 | 处理请求的时间（毫秒） |
| 模块类型 | 字符串 | Variant、Stream或VOD |
| remote_address_aud_client_ip | 字符串 | **‡** |
| remote_address_x_fwd_for_hdr_key | 字符串 | **‡** |
| remote_host_port | 字符串 | **‡** |

**‡** 后三个字段是可选的。

**示例**

```shell
1427263800524 6495aafc-3f34-4047-ad36-350d4f056eb4 189938TRACE_REQUEST_INFO 301 GET /auditude/variant/pubAsset/aHR0cDov. . ..m3u8?u=cecebae72a919de350b9ac52602623f3&z=189938&ptcueformat=turner& sid =yk-cnnlive-003 &ptdebug=true 0 0 0 Variant 111.22.3.44 111.22.3.45 127.0.0.1:46383
```

### TRACE_HTTP_HEADER记录 {#trace-http-header-records}

此类型的记录记录记录清单服务器和客户端、广告服务器或内容服务器之间的HTTP调用期间交换的HTTP标头。 TRACE_HTTP_HEADER以外的字段按表中显示的顺序显示，用制表符分隔。

| 字段 | 类型 | 描述 |
|---|---|---|
| request_type | 字符串 | 请求类型（MAIN或UNKNOWN） |
| request_response | 字符串 | 响应标头（请求或响应） |
| header_name | 字符串 | HTTP标头名称 |
| 标头值 | 字符串 | Base64编码的HTTP标头值 |

>[!NOTE]
>
>此 `request_type` 和 `header_value` 字段是可选的。

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

### TRACEAD_CALL记录 {#tracing-ad-call-records}

此类型的记录记录记录清单服务器和请求的结果。 字段超出 `TRACE_AD_CALL` 按表中显示的顺序显示，用制表符分隔。

| 字段 | 类型 | 描述 |
|---|---|---|
| 状态 | 字符串 | 返回的HTTP状态代码 |
| request_duration | 整数 | 从请求到响应的时间（毫秒） |
| ad_server_query_url | 字符串 | 广告调用的URL，包括查询参数 |
| ad_system_id | 字符串 | 广告系统，来自广告服务器响应（如果未指定，则为审计） |
| avail_id | 字符串 | 从内容清单文件中的广告提示开始的可用的ID（对于VOD，不适用） |
| avail_duration | 数字 | 从内容清单文件中的广告提示开始的可用持续时间（秒）（对于VOD，不适用） |
| ad_server_response | 字符串 | 来自广告服务器的Base64编码响应 |

示例：

```shell
2015-03-25T06:13:31.271Z 14272. . . 189938 TRACE_AD_CALL200 8 https://ad.stg2.auditude.com/adserver/a?cip=0.0.0.0&g=1000012&of=1.5 &ptcueformat=turner&ptdebug=true&tl=l,150,30,m&tm=63&u=ceceb. . . Auditude IvpIyC. . . 150 PD94bWw. . .
```

### TRACEAD_INSERT、TRACEAD_RESOLVE和TRACEAD_REDIRECT记录 {#trace-ad-insert-resolve-redirect}

此类型的记录记录记录记录记录类型指示的广告请求的结果。 记录类型以外的字段按表中显示的顺序显示，用制表符分隔。

| 字段 | 类型 | 描述 |
|---|---|---|
| 状态 | 字符串 | 返回了HTTP状态代码。 |
| avail_id | 字符串 | 可用的ID，来自内容清单文件(live)中的广告提示或来自清单服务器(VOD)。 |
| ad_type | 字符串 | 广告类型（直接或重定向）。 |
| ad_duration | 整数 | 广告的持续时间（秒），来自广告服务器响应。 |
| ad_content_url | 字符串 | 广告的清单文件的URL，来自广告服务器响应。 |
| **†** ad_content_url_actual | 字符串 | 插入广告的清单文件的URL。 对于TRACE_AD_REDIRECT，留空。 |
| ad_system_id | 字符串 | 广告系统，来自广告服务器响应（如果未指定，则为Auditude）。 |
| ad_id | 字符串 | 广告的ID，来自广告服务器响应。 |
| creative_id | 字符串 | 广告服务器响应中广告节点的创意ID。 |
| **†** ad_call_id | 字符串 | 未使用。 保留供将来使用。 |
| delta | 整数 | 此事件所用的时间（毫秒）。 |
| **†** 杂项 | 字符串 | 跳过广告的原因。 |

**†** `ad_content_url_actual`， `ad_call_id`、和 `misc` 字段是可选的。

>[!NOTE]
>
>对象 `TRACE_AD_RESOLVE` 和 `TRACE_AD_INSERT`，中的URL `ad_content_url_actual` 字段适用于已转码广告（如果可用）。 否则，字段为空 `TRACE_AD_RESOLVE` 或与 `ad_content_url` 对象 `TRACE_AD_INSERT`.

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

### TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE记录 {#trace-transcoding-no-media-to-transcode}

此类型的记录记录记录缺失的广告创意。 唯一超出的字段 `TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE` 显示在表中。

| 字段 | 类型 | 描述 |
|---|---|---|
| ad_id | 字符串 | 完全限定的广告ID (FQ_AD_ID： Q_AD_ID\[；Q_AD_ID\[；Q_AD_ID...\] \] Q_AD_ID：协议:AD_SYSTEM:AD_ID\[：CREATIVE_ID\[：MEDIA_ID\] \]协议：AUDITUDE，VAST) |

此类型的记录记录记录清单服务器发送到CRS的代码转换请求的结果。 字段超出 `TRACE_TRANSCODING_REQUESTED` 按表中显示的顺序显示，用制表符分隔。

| 字段 | 类型 | 描述 |
|---|---|---|
| ad_id | 字符串 | 完全限定的广告ID |
| ad_manifest_url | 字符串 | 广告清单文件的URL，来自广告服务器响应 |
| creative_type | 字符串 | 媒体类型 |
| 标志 | 字符串 | ID3指示转码请求是否包含添加ID3标记的请求 |
| target_duration | 字符串 | 转码创意的目标持续时间（秒） |

此类型的记录指示执行服务器端跟踪的请求。 字段超出 `TRACE_TRACKING_REQUEST` 按表中显示的顺序显示，用制表符分隔。

| 字段 | 类型 | 描述 |
|---|---|---|
| tracking_url_count | 整数 | 跟踪URL的数量 |
| 开始 | 浮点数 | PTS片段开始时间（以毫秒为精度单位，以秒为单位） |
| 结束 | 浮点数 | PTS片段结束时间（以毫秒为精度单位，以秒为单位） |

此类型的记录为服务器端跟踪提供跟踪URL。 字段超出 `TRACE_TRACKING_REQUEST_URL` 按表中显示的顺序显示，用制表符分隔。

| 字段 | 类型 | 描述 |
|---|---|---|
| 时间戳 | 浮点数 | 播放会话中用于ping跟踪URL的时间（以秒为单位，精确度为。001）。 |
| ad_system | 字符串 | 广告系统（例如，auditude） |
| url | 字符串 | ping的URL |

清单服务器发出的此类型日志请求记录 `WEBVTT` 字幕。 字段超出 `TRACE_WEBVTT_REQUEST` 按表中显示的顺序显示，用制表符分隔。

| 字段 | 类型 | 描述 |
|---|---|---|
| 状态 | 字符串 | 返回的HTTP状态代码 |
| vtt_uri | 字符串 | 请求的URL |
| 开始 | 浮点数 | 拆分开始时间（以毫秒为精确度计算的秒数） |
| 结束 | 浮点数 | 拆分结束时间（以毫秒为精确度计算的秒数） |

清单服务器发送到客户端的此类日志响应记录 `answer` 至请求 `WEBVTT` 字幕。 字段超出 `TRACE_WEBVTT_RESPONSE` 按表中显示的顺序显示，用制表符分隔。

| 字段 | 类型 | 描述 |
|---|---|---|
| 状态 | 字符串 | 返回的HTTP状态代码 |
| 响应 | 字符串 | 发送到客户端的Base64编码响应 |

此类型的记录响应清单服务器发出的请求 `WEBVTT` 字幕。 字段超出 `TRACE_WEBVTT_SOURCE` 按表中显示的顺序显示，用制表符分隔。

| 字段 | 类型 | 描述 |
|---|---|---|
| 状态 | 字符串 | 返回的HTTP状态代码 |
| 源 | 字符串 | Base64编码的原始VTT内容 |

此类型的记录使清单服务器能够在摄取广告时记录除此之外未计划的事件和信息。 字段超出 `TRACE_MISC` 由消息字符串组成。 可能显示的消息包括：

* 已忽略广告：AdPlacement \[adManifestURL=https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb。...m3u8， durationSeconds=15.0， ignore=false， redirectAd=false， priority=1\]
* AdPlacement adManifestURL= adManifestURL， durationSeconds=秒， ignore=忽略， redirectAd= redirectAd， priority=优先级
* 广告投放返回了null。
* 广告已成功拼接。
* 广告调用失败：错误消息。
* 正在添加User-Agent以获取原始清单： user-agent。
* 正在添加Cookie以获取原始清单： #
* 请求的URL错误URL错误消息。 （未能分析变体URL）
* 调用的URL： URL得到return：响应代码。 （实时URL）
* 调用的url： URL返回代码：响应代码。 ( VOD URL)
* 解决广告时发现冲突：中置开始时间或中置结束时间之一位于中置(VOD)中包含的前置或前置中。
* 检测到URI：请求URL的处理程序引发的未处理异常。
* 已完成生成变量清单。 （变量）
* 已完成生成变量清单。
* 处理VAST重定向*重定向URL *错误：错误消息时出现异常。
* 未能获取广告清单URL的广告播放列表。
* 未能生成目标清单。 (HLSManifestResolver)
* 未能分析第一个广告调用响应：错误消息。
* 无法处理*GET|POST*对path：请求URL的请求。 （实时/VOD）
* 无法处理实时清单请求：请求URL。 （正式启用）
* 无法返回变体清单：错误消息。
* 无法验证组ID：组ID。
* 正在获取原始清单：内容URL。 （正式启用）
* 以下VAST重定向：重定向URL。
* 发现空可用。 (VOD)
* 已找到 *数字* 广告。 (VOD)
* 已收到HTTP请求。 （第一条消息）
* 忽略广告，因为广告响应持续时间（*广告响应持续时间*秒）与实际广告持续时间（*实际持续时间*秒）之间的差异大于限制。 (HLSManifestResolver)
* 忽略未提供ID值的值。 (GroupAdResolver.java)
* 忽略提供无效时间值的可用性： *time *对于availId =可用ID。
* 忽略提供无效持续时间值的可用性： *duration *表示可用ID =可用ID。
* 初始化新会话。 （变量）
* HTTP方法无效。 它必须是GET。 (VOD)
* HTTP方法无效。 跟踪请求必须为GET。 （正式启用）
* 请求的URL无效URL错误消息。 （变量）
* 组无效。 (HLSManifestResolver)
* 请求无效。 字幕不是有效的跟踪请求。 (VOD)
* 请求无效。 必须在建立会话后发出字幕请求。 (VOD)
* 请求无效。 必须在建立会话后发出跟踪请求。 (VOD)
* 重载组ID的服务器实例无效：组ID。 （正式启用）
* 已达到VAST重定向数限制 — 数字。
* 进行广告调用：广告调用URL。
* 未找到以下内容的清单：内容URL。 （正式启用）
* 未找到可用ID的匹配可用项：可用ID。 (HLSManifestResolver)
* 未找到播放会话。 (HLSManifestResolver)
* 正在处理清单内容URL的VOD请求。
* 正在处理变量。
* 正在处理清单内容URL的字幕请求。
* 正在处理跟踪请求。 (VOD)
* 重定向广告响应为空。 ( VASTStAX)
* 请求： URL。
* 正在返回GET请求的错误响应，因为未找到播放会话。 (VOD)
* 由于内部服务器错误，返回了GET请求的错误响应。
* 返回指定无效资源的GET请求的错误响应：广告请求ID。 (VOD)
* 为指定无效或空的组ID的GET请求返回错误响应：组ID。 (VOD)
* 正在返回指定无效GET位置值的跟踪请求的错误响应。 (VOD)
* 使用无效语法返回GET请求的错误响应 — 请求URL。 （实时/VOD）
* 使用不支持的HTTP方法返回请求的错误响应：GET|POST。 （实时/VOD）
* 正在从缓存返回清单。 (VOD)
* 服务器超载。 无需广告拼接请求即可继续。 （变量）
* 开始生成目标清单。 (HLSManifestResolver)
* 开始从以下来源生成变体清单：内容URL。 （变量）
* 开始将广告拼接到清单中。 (VODHLSResolver)
* 尝试拼接广告 `HH:MM:SS`：AdPlacement \[adManifestURL=广告清单URL，durationSeconds=秒，ignore=忽略，redirectAd=重定向广告，priority=优先级。\] \(HLSManifestResolver\)
* 由于时间轴无效，无法获取广告 — 返回了没有广告的内容。 (VOD)
* 无法获取广告 — 返回了没有广告的内容。 (VOD)
* 无法获取广告查询，但未提供内容URL。 (VOD)
* 收到有效的URL。 （VOD/变量）
* 未找到变量M3U8。 （变量）

### TRACE播放进度记录 {#trace-playback-progress-records}

清单服务器在服务器端跟踪工作流期间接收到有关播放进度的信号时生成此类记录。 字段超出 `TRACE_PLAYBACK_PROGRESS` 按表中显示的顺序显示，用制表符分隔。

| 字段 | 类型 | 描述 |
|---|---|---|
| 状态 | 字符串 | HTTP状态代码 |
| 带宽 | 整数 | 流的带宽 |
| 分 | 整数 | 流中的PTS时间 |
| ms_time | 整数 | 清单服务器生成跟踪网址的时间 |
| url | 字符串 | 重定向URL |
| **？** header_user_agent | 字符串 | HTTP User-Agent标头 |
| **？** header_dnt | 整数 | HTTP do-not-track头 |
| **？** effective_remote_address | 字符串 | IPv4有效的远程地址 |
| **？** remoteaddress | 字符串 | IPv4远程地址 |

**？** 后四个字段是可选的。

## 多比特率流 {#multiple-bitrate-streams}

广告插入的客户端请求通常在变体M3U8格式的播放列表中指定一个以上的比特率。 清单服务器生成并返回一个新的变体M3U8文件，该文件包含用于每个比特率的单独M3U8链接。 它还生成唯一的组ID以将这些M3U8绑定在一起。

清单服务器使用客户端BootstrapURL请求中的信息来检索内容变体播放列表。 它生成一个新的变体播放列表，其中包含指向流级别内容的清单服务器链接。 客户端使用这些插件来构建广告插入请求。 清单服务器的流级别内容链接具有以下格式：

```shell
https://manifest.auditude.com/auditude/{live/vod}/{publisherAssetID}/{rendition}/
{groupID}/{base64-encoded url of the bit rate stream}.[m3u8]?{Query parameters}
```

* **live/vod**
清单服务器根据内容的播放列表类型设置此值：实时/线性(
`#EXT-X-PLAYLIST-TYPE:EVENT`)或VOD (`#EXT-X-PLAYLIST-TYPE:VOD`)

* **publisherAssetID**
BootstrapURL请求中提供的特定内容的发布者唯一ID。

* **演绎版**
清单服务器根据 
`BANDWIDTH` 值，并使用它来匹配广告的比特率与内容的比特率。 广告比特率不能超过内容的比特率，除非具有最低比特率的广告演绎版这样做。

* **groupID**
清单服务器会生成此值并使用它来确保无论客户端请求广告的位速率演绎版为何，都始终如一地放置广告。

* **比特率流的base64编码url**
清单服务器URL安全的base64对内容流的绝对URL进行编码。 每个流都有自己的URL。

* **查询参数**
BootstrapURL请求中提供的查询参数。
