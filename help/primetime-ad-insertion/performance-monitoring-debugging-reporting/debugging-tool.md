---
title: 清单服务器调试工具
description: 清单服务器调试工具
products: SG_PRIMETIME
topic-tags: ad-insertion
discoiqdonotlocalize: false
moreHelpPaths: /content/help/en/primetime/morehelp/ad-insertion;/content/help/en/primetime/morehelp/ad-insertion
pagecreatedat: en
pagelayout: video
sidecolumn: left
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '2414'
ht-degree: 0%

---


# 清单服务器调试工具 {#manifest-server-debugging-tool}

调试工具使发布者能够通过检查清单服务器在HTTP标头中实时返回的调试信息，或者在需要更多详细信息时，在事后检查会话日志，来调查可能代价高昂的广告插入问题。 像Akamai这样的Adobe合作伙伴可以使用此工具来调试他们与Primetime ad decisioning的集成。

该工具支持在任何主要清单服务器和跟踪配置中进行调试和插入问题：

* 使用基于TVSDK的播放器跟踪客户端。
* 使用不基于TVSDK的播放器进行客户端跟踪。
* 服务器端跟踪。

要支持所有这些情况，该工具不需要或使用播放器发布器代码。

在启动清单服务器会话时，您可以在请求URL上设置参数，以要求它记录调试信息。 使用该参数的不同值，您还可以要求清单服务器在HTTP标头中返回指定的调试信息段，但标头只能包含有限数量的信息。 您可以从Adobe获取凭据以访问完整的日志文件，清单服务器定期（例如，每小时）将日志文件保存在存档服务器上。 一旦您拥有该服务器的凭据，您就可以随时直接访问它。

<!-- You can also see the [server side event tracking captured in the SSAI dashboard](ssai-debugging-dashboard.md).-->

## 调试工具选项 {#debugging-tool-options}

在调用调试工具时，对于清单服务器在HTTP标头中返回的信息，您有多个选项。 这些选项不会影响清单服务器在日志文件中放置的内容。

### 指定ptdebug {#specifying-ptdebug}

在启动清单服务器会话的调试日志记录时，可以将ptdebug参数添加到请求URL中，以便为清单服务器在HTTP标头中返回的信息指定以下选项：

* ptdebug=true除外的所有记录 `TRACE_HTTP_HEADER` 和最多 `call/response data` 起始日期 `TRACE_AD_CALL` 记录。
* ptdebug=AdCall OnlyTRACE_AD_*type* (例如，TRACE_AD_CALL)记录。
* ptdebug=Header OnlyTRACE_HTTP_HEADER记录。

这些选项不会影响清单服务器在日志文件中放置的内容。 您对此没有控制权，但日志文件是文本文件，因此您可以应用各种工具来提取和重新格式化您感兴趣的信息。

以下是以下情况下返回的HTTP标头的示例 `ptdebug=Header`. 一些十六进制数字的长字符串将被替换为 `. . .` 为了清楚起见。

```
X-ADBE-AI-DBG-1 TRACE_MISC    HTTP request received
X-ADBE-AI-DBG-2 TRACE_MISC    Processing Variant
X-ADBE-AI-DBG-3 TRACE_MISC    Valid URL received.
X-ADBE-AI-DBG-4 TRACE_MISC    Initialize new session
X-ADBE-AI-DBG-5 TRACE_MISC    Requesting: /auditude/variant/pubAsset/aHR0cDovL . . .m3u8
 ?u=cecebae . . .&z=189962&pttrackingmode=simple&pttrackingversion=v1
 &ptcueformat=turner&__sid__=yk-sat953pm-112
 &ptdebug=true
X-ADBE-AI-DBG-6  TRACE_HTTP_HEADER  MAIN  REQUEST  Host    bWFuaWZl. . .
X-ADBE-AI-DBG-7  TRACE_HTTP_HEADER  MAIN  REQUEST  Connection       Y2xvc2U=
X-ADBE-AI-DBG-8  TRACE_HTTP_HEADER  MAIN  REQUEST  Accept   dGV4dC. . .
X-ADBE-AI-DBG-9  TRACE_HTTP_HEADER  MAIN  REQUEST  Cookie   c3NhaT. . .
X-ADBE-AI-DBG-10 TRACE_HTTP_HEADER  MAIN  REQUEST  User-Agent       TW96aWxs. . .
X-ADBE-AI-DBG-11 TRACE_HTTP_HEADER  MAIN  REQUEST  Accept-Language  ZW4tdXM=
X-ADBE-AI-DBG-12 TRACE_HTTP_HEADER  MAIN  REQUEST  Accept-Encoding  Z3ppcCwg. . .=
X-ADBE-AI-DBG-13 TRACE_REQUEST_INFO  200   GET
 /auditude/variant/pubAsset/aHR0cD. . ..m3u8
 ?u=cecebae72a919de350b9ac52602623f3&z=189962&pttrackingmode=simple
 &pttrackingversion=v1&ptcueformat=turner&__sid__=yk-sat953pm-112
 &ptdebug=true   0 0 0   Variant  NA  null  null  127.0.0.1:43357
X-ADBE-AI-DBG-14 TRACE_HTTP_HEADER  MAIN  RESPONSE Content-Type     YXBwbG. . .
X-ADBE-AI-DBG-15 TRACE_HTTP_HEADER  MAIN  RESPONSE Cache-Control    bm8tY2. . .
X-ADBE-AI-DBG-16 TRACE_HTTP_HEADER  MAIN  RESPONSE Access-Control-Allow-Origin    Kg==
X-ADBE-AI-DBG-17 TRACE_MISC   Done
```

## 日志记录的格式 {#formats-of-log-records}

每个日志记录都有一个类型和一组字段，其中一些字段可能是可选的。 记录类型之前的所有记录的字段是相同的。 它们提供时间戳和有关会话的信息。 记录类型标识所记录的事件类型，后续字段提供有关所记录事件的信息。

日志记录的结构如下：

`datetime request_id session_id zone_id record_type` *其他字段。*

| 字段 | 类型 | 描述 |
|--- |--- |--- |
| datetime | 字符串 | 时间戳 |
| request_id | 字符串 | 清单服务器使用的请求ID （unix时间戳） |
| session_id | 字符串 | 清单服务器使用的会话ID |
| zone_id | 整数 | 区域Id |
| record_type | 字符串 | 所记录的事件类型 |
| 其他字段 | *** | 取决于事件类型 |

### TRACE请求信息记录 {#trace-request-info-records}

此类型的记录记录HTTP请求的结果。 超出TRACE_REQUEST_INFO的字段按表中显示的顺序显示，以制表符分隔。

| 字段 | 类型 | 描述 |
|--- |--- |--- |
| 状态 | 字符串 | 返回的HTTP状态代码 |
| request_method | 字符串 | HTTP方法(GET或POST) |
| request_uri | 字符串 | HTTP请求URI（不带主机） |
| request_length | 整数 | 请求长度（字节） |
| response_length | 整数 | 响应长度（字节） |
| delta | 整数 | 处理请求的时间（毫秒） |
| 模块类型 | 字符串 | Variant、Stream或VOD |
| remote_address_aud_client_ip | 字符串 | （见注释） |
| remote_address_x_fwd_for_hdr_key | 字符串 | （见注释） |
| remote_host_port | 字符串 | （见注释） |

>[!NOTE]
>
>后三个字段是可选的。

示例：

```
1427263800524 6495aafc-3f34-4047-ad36-350d4f056eb4 189938
TRACE_REQUEST_INFO 301 GET /auditude/variant/pubAsset/aHR0cDov. . ..m3u8
?u=cecebae72a919de350b9ac52602623f3&z=189938&ptcueformat=turner& sid =yk-cnnlive-003 &ptdebug=true 0 0 0 Variant 111.22.3.44 111.22.3.45 127.0.0.1:46383
```

### TRACE_HTTP_HEADER记录 {#trace-http-header-records}

此类型的记录记录记录清单服务器和客户端、广告服务器或内容服务器之间的HTTP调用期间交换的HTTP标头。 TRACE_HTTP_HEADER以外的字段按表中显示的顺序显示，用制表符分隔。

| 字段 | 类型 | 描述 |
|--- |--- |--- |
| request_type | 字符串 | 请求类型（MAIN或UNKNOWN） |
| request_response | 字符串 | 响应标头（请求或响应） |
| header_name | 字符串 | HTTP标头名称 |
| 标头值 | 字符串 | Base64编码的HTTP标头值 |

>[!NOTE]
>
>request_type和header_value字段是可选的。

示例：

```
2015-03-25T06:10:00.927Z  1427263800573  6495aa. . .  189938 TRACE_MISC
    Requesting: /cnn/tvecnn/stream4/stream_Layer.m3u8
2015-03-25T06:10:00.927Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN REQUEST Cookie  aGRu. . .
2015-03-25T06:10:00.928Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN REQUEST User-Agent  TW96aW. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Server  bmd4X2. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Content-Type    YXBwb. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Last-Modified   V2VkL. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  ETag    IjIyY2. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Vary    QWNjZXB. . .
2015-03-25T06:10:01.063Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Cache-Control   bWF4LW. . .
2015-03-25T06:10:01.064Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Expires V2VkL. . .
2015-03-25T06:10:01.064Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Date    V2VkLCA. . .
2015-03-25T06:10:01.064Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Age MQ==
2015-03-25T06:10:01.064Z  1427263800573  6495aa. . .  189938 TRACE_HTTP_HEADER
    UNKNOWN RESPONSE  Via MS4xIH. . .
```

### TRACEAD_CALL记录 {#trace-ad-call-records}

此类型的记录记录记录清单服务器和请求的结果。 TRACE_AD_CALL以外的字段按表中显示的顺序显示，并以制表符分隔。

| 字段 | 类型 | 描述 |
|--- |--- |--- |
| 状态 | 字符串 | 返回的HTTP状态代码 |
| request_duration | 整数 | 从请求到响应的时间（毫秒） |
| ad_server_query_url | 字符串 | 广告调用的URL，包括查询参数 |
| ad_system_id | 字符串 | 广告系统，来自广告服务器响应（如果未指定，则为审计） |
| avail_id | 字符串 | 从内容清单文件中的广告提示开始的可用的ID（对于VOD，不适用） |
| avail_duration | 数字 | 从内容清单文件中的广告提示开始的可用持续时间（秒）（对于VOD，不适用） |
| ad_server_response | 字符串 | 来自广告服务器的Base64编码响应 |

示例：

```
2015-03-25T06:13:31.271Z 14272. . . 189938 TRACE_AD_CALL
200 8 https://ad.stg2.auditude.com/adserver/a?cip=0.0.0.0&g=1000012&of=1.5 &ptcueformat=turner&ptdebug=true&tl=l,150,30,m&tm=63&u=ceceb. . . Auditude IvpIyC. . . 150 PD94bWw. . .
```

### TRACEAD_INSERT、TRACEAD_RESOLVE和TRACEAD_REDIRECT记录 {#trace-ad-insert-trace-ad-resolve-and-trace-ad-redirect-records}

此类型的记录记录记录记录记录类型指示的广告请求的结果。 记录类型以外的字段按表中显示的顺序显示，用制表符分隔。

| 字段 | 类型 | 描述 |
|--- |--- |--- |
| 状态 | 字符串 | 返回的HTTP状态代码 |
| avail_id | 字符串 | 可用的ID，来自内容清单文件(live)中的广告提示或来自清单服务器(VOD) |
| ad_type | 字符串 | 广告类型（直接或重定向） |
| ad_duration | 整数 | 广告的持续时间（秒），来自广告服务器响应 |
| ad_content_url | 字符串 | 广告清单文件的URL，来自广告服务器响应 |
| ad_content_url_actual | 字符串 | 插入广告的清单文件的URL。 对于TRACE_AD_REDIRECT，留空。 |
| ad_system_id | 字符串 | 广告系统，来自广告服务器响应（如果未指定，则为审计） |
| ad_id | 字符串 | 广告的ID，来自广告服务器响应 |
| creative_id | 字符串 | 广告节点和广告服务器响应中的创意ID |
| ad_call_id | 字符串 | 未使用。 保留供将来使用。 |
| delta | 整数 | 此事件所用的时间（毫秒） |
| 杂项 | 字符串 | 跳过广告的原因 |

>[!NOTE]
>
>ad_content_url_actual、ad_call_id和misc字段是可选的。

对于TRACE_AD_RESOLVE和TRACE_AD_INSERT，ad_content_url_actual字段中的URL适用于转码广告（如果可用）。 否则，对于TRACE_AD_RESOLVE，该字段为空，或者与TRACE_AD_INSERT的ad_content_url相同。

示例：

```
2015-03-18T22:25:36.229-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_RESOLVE
200 0 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 Auditude 308008 0  cecebae72a919de350b9ac52602623f3 0 NA

2015-03-18T22:25:36.230-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_RESOLVE
200 2 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 Auditude 308008 0  cecebae72a919de350b9ac52602623f3 0 NA

2015-03-18T22:25:36.562-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_INSERT
200 0 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8
Auditude 308008 0 cecebae72a919de350b9ac52602623f3 0 NA
2015-03-18T22:25:36.563-07:00 1426742736208 1120feb. . . 147465 TRACE_AD_INSERT
200 2 DIRECT 15 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8 https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . ..m3u8
Auditude 308008 0 cecebae72a919de350b9ac52602623f3 0 NA
```

### TRACE_TRACKING_URL记录 {#trace-tracking-url-records}

此类型的记录记录记录清单服务器和请求的结果。 TRACE_TRACKING_URL以外的字段按表中显示的顺序显示，并以制表符分隔。

| 字段 | 类型 | 描述 |
|--- |--- |--- |
| 分 | 数字 | 项目时间戳。 在视频中调用URL所需的时间。 |
| ad_system | 字符串 | 广告系统（受众或自由轮） |
| url | 字符串 | URL已钉选 |
| 状态 | 字符串 | ping返回的HTTP状态 |

示例：

```
2015-06-04T23:24:42.000-0700    1426742736208     3086f5cd . . .    12345    TRACE_TRACKING_URL
    0.000000    ExampleSystem    https://localhost/index.php?stream:test#8.1433485415;
    sid:3086f5cd . . .;pts:0    200
```

### TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE记录 {#trace-transcoding-no-media-to-transcode-records}

此类型的记录记录记录缺失的广告创意。 TRACE_TRANSCODING_NO_MEDIA_TO_TRANSCODE之外的唯一字段显示在表中。

| 字段 | 类型 | 描述 |
|--- |--- |--- |
| ad_id | 字符串 | 完全限定的广告ID `(FQ_AD_ID: Q_AD_ID\[;Q_AD_ID\[;Q_AD_ID...\]\]` Q_AD_ID： `PROTOCOL:AD_SYSTEM:AD_ID\[:CREATIVE_ID\[:MEDIA_ID\]\]` 协议：AUDITUDE，VAST) |

### TRACE_转码_请求记录 {#trace-transcoding-requested-records}

此类型的记录记录记录清单服务器发送到CRS的代码转换请求的结果。 超出TRACE_TRANSCODING_REQUESTED的字段按表中显示的顺序显示，用制表符分隔。

| 字段 | 类型 | 描述 |
|--- |--- |--- |
| ad_id | 字符串 | 完全限定的广告ID |
| ad_manifest_url | 字符串 | 广告清单文件的URL，来自广告服务器响应 |
| creative_type | 字符串 | 媒体类型 |
| 标志 | 字符串 | ID3指示转码请求是否包含添加ID3标记的请求 |
| target_duration | 字符串 | 转码创意的目标持续时间（秒） |

### TRACE跟踪请求记录 {#trace-tracking-request-records}

此类型的记录指示执行服务器端跟踪的请求。 超出TRACE_TRACKING_REQUEST的字段按表中显示的顺序显示，并以制表符分隔。

| 字段 | 类型 | 描述 |
|--- |--- |--- |
| tracking_url_count | 整数 | 跟踪URL的数量 |
| 开始 | 浮点数 | PTS片段开始时间（以毫秒为精度单位，以秒为单位） |
| 结束 | 浮点数 | PTS片段结束时间（以毫秒为精度单位，以秒为单位） |

### TRACE_TRACKING_REQUEST_URL记录 {#trace-tracking-request-url-records}

此类型的记录为服务器端跟踪提供跟踪URL。 超出TRACE_TRACKING_REQUEST_URL的字段按表中显示的顺序显示，并以制表符分隔。

| 字段 | 类型 | 描述 |
|--- |--- |--- |
| 时间戳 | 浮点数 | 播放会话中ping跟踪URL的时间（以秒为单位，精确度为。001） |
| ad_system | 字符串 | 广告系统（例如，auditude） |
| url | 字符串 | ping的URL |

### TRACE_WEBVTT_REQUEST记录 {#trace-webvtt-request-records}

此类型日志的记录请求清单服务器发出WEBVTT字幕。 TRACE_WEBVTT_REQUEST以外的字段按表中显示的顺序显示，用制表符分隔。

| 字段 | 类型 | 描述 |
|--- |--- |--- |
| 状态 | 字符串 | 返回的HTTP状态代码 |
| vtt_uri | 字符串 | 请求的URL |
| 开始 | 浮点数 | 拆分开始时间（以毫秒为精确度计算的秒数） |
| 结束 | 浮点数 | 拆分结束时间（以毫秒为精确度计算的秒数） |

### TRACE_WEBVTT_RESPONSE记录 {#trace-webvtt-response-records}

记录 ``of ``此 ``type ``log ``responses ``此 ``manifest ``服务器 ``sends ``到 ``clients ``在 `` `answer` ``到 ``requests `` `for` ``WEBVTT ``字幕。 TRACE_WEBVTT_RESPONSE &quot;以外的字段按表中显示的顺序显示，以分隔 `by`选项卡。

| 字段 | 类型 | 描述 |
|--- |--- |--- |
| 状态 | 字符串 | 返回的HTTP状态代码 |
| 响应 | 字符串 | 发送到客户端的Base64编码响应 |

### TRACE_WEBVTT_SOURCE记录 {#trace-webvtt-source-records}

此类型的记录记录响应清单服务器发出的WEBVTT字幕请求。 TRACE_WEBVTT_SOURCE以外的字段按表中显示的顺序显示，以制表符分隔。

| 字段 | 类型 | 描述 |
|--- |--- |--- |
| 状态 | 字符串 | 返回的HTTP状态代码 |
| 源 | 字符串 | Base64编码的原始VTT内容 |


### TRACE_MISC记录 {#trace-misc-records}

此类型的记录使清单服务器能够在摄取广告时记录除此之外未计划的事件和信息。 TRACE_MISC之外的字段由消息字符串组成。 可能显示的消息包括：

* 忽略的广告：AdPlacement `[adManifestURL=https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . . .m3u8, durationSeconds=15.0, ignore=false, redirectAd=false, priority=1]`
* AdPlacement adManifestURL=*adManifestURL*， durationSeconds=*秒*，忽略=*忽略*，redirectAd=*redirectAd*，优先级=*优先级*
* 广告投放返回了null。
* 广告已成功拼接。
* 广告调用失败： *错误消息*.
* 正在添加User-Agent以获取原始清单： *user-agent*.
* 添加Cookie以获取原始清单： [Cookie]
* 错误的URL *请求的URL错误消息*. （未能分析变体URL）
* 调用的url： URL *get return： response code*. （实时URL）
* 调用的url： URL *返回代码：响应代码*. ( VOD URL)
* 解决广告时发现冲突：中置开始时间或中置结束时间之一位于中置(VOD)中包含的前置或前置中。
* 检测到URI的处理程序引发的未处理异常： *请求URL*.
* 已完成生成变量清单。 （变量）
* 已完成生成变量清单。
* 处理VAST重定向*重定向URL *错误时出现异常： *错误消息*.
* 未能获取广告的播放列表 *广告清单URL*.
* 未能生成目标清单。 (HLSManifestResolver)
* 未能分析第一个广告调用响应： *错误消息*.
* 无法处理*GET|POST*路径请求： *请求URL*. （实时/VOD）
* 无法处理实时清单请求： *请求URL*. （正式启用）
* 无法返回变量清单： *错误消息*.
* 无法验证组ID： *组标识*.
* 正在获取原始清单： *内容URL*. （正式启用）
* 以下VAST重定向： *重定向URL*.
* 发现空可用。 (VOD)
* 找到*number *ads。 (VOD)
* 已收到HTTP请求。 （第一条消息）
* 忽略广告，因为广告响应持续时间（*广告响应持续时间*秒）与实际广告持续时间（*实际持续时间*秒）之间的差异大于限制。 (HLSManifestResolver)
* 忽略未提供ID值的值。 (GroupAdResolver.java)
* 忽略提供无效时间值的可用性： *时间*对于availId = *可用ID*.
* 忽略提供无效持续时间值的可用性： *duration *表示availId = *可用ID*.
* 初始化新会话。 （变量）
* HTTP方法无效。 它必须是GET。 (VOD)
* HTTP方法无效。 跟踪请求必须为GET。 （正式启用）
* URL无效 *请求的URL错误消息*. （变量）
* 组无效。 (HLSManifestResolver)
* 请求无效。 字幕不是有效的跟踪请求。 (VOD)
* 请求无效。 必须在建立会话后发出字幕请求。 (VOD)
* 请求无效。 必须在建立会话后发出跟踪请求。 (VOD)
* 重载组ID的服务器实例无效： *组标识*. （正式启用）
* 已达到VAST重定向限制 —  *数字*.
* 进行广告调用： *广告调用URL*.
* 未找到以下项的清单： *内容URL*. （正式启用）
* 未找到可用ID的匹配可用： *可用ID*. (HLSManifestResolver)
* 未找到播放会话。 (HLSManifestResolver)
* 正在处理清单的VOD请求 *内容URL*.
* 正在处理变量。
* 正在处理清单的字幕请求 *内容URL*.
* 正在处理跟踪请求。 (VOD)
* 重定向广告响应为空。 ( VASTStAX)
* 请求： *URL*.
* 正在返回GET请求的错误响应，因为未找到播放会话。 (VOD)
* 由于内部服务器错误，返回了GET请求的错误响应。
* 返回指定无效资源的GET请求的错误响应： *广告请求编号*. (VOD)
* 为指定无效或空的组ID的GET请求返回错误响应： *组标识*. (VOD)
* 正在返回指定无效GET位置值的跟踪请求的错误响应。 (VOD)
* 使用无效语法返回GET请求的错误响应 —  *请求URL*. （实时/VOD）
* 使用不支持的HTTP方法返回请求的错误响应： *GET|POST*. （实时/VOD）
* 正在从缓存返回清单。 (VOD)
* 服务器超载。 无需广告拼接请求即可继续。 （变量）
* 开始生成目标清单。 (HLSManifestResolver)
* 开始从以下来源生成变体清单： *内容URL*. （变量）
* 开始将广告拼接到清单中。 (VODHLSResolver)
* 尝试拼接广告 `HH:MM:SS`：AdPlacement \[adManifestURL=*广告清单URL*， durationSeconds=*秒*，忽略=*忽略*，redirectAd=*重定向广告*，优先级=*优先级*.\]
* 由于时间轴无效，无法获取广告 — 返回了没有广告的内容。 (VOD)
* 无法获取广告 — 返回了没有广告的内容。 (VOD)
* 无法获取广告查询，但未提供内容URL。 (VOD)
* 收到有效的URL。 （VOD/变量）
* 未找到变量M3U8。 （变量）

### TRACE_TRACKING_URL记录 {#trace-tracking-url-records-1}

清单服务器在服务器端跟踪工作流中调用跟踪URL后生成此类记录。 TRACE_TRACKING_URL以外的字段按表中显示的顺序显示，并以制表符分隔。

| 字段 | 类型 | 描述 |
|--- |--- |--- |
| 分 | 数字 | 流中的PTS时间 |
| ad_system | 字符串 | 广告系统（受众或自由轮） |
| url | 字符串 | URL已钉选 |
| state | 字符串 | HTTP状态代码 |

### TRACE播放进度记录 {#trace-playback-progress-records}

清单服务器在服务器端跟踪工作流期间接收到有关播放进度的信号时生成此类记录。 超出TRACE_PLAYBACK_PROGRESS的字段按表中显示的顺序显示，以制表符分隔。

| 字段 | 类型 | 描述 |
|--- |--- |--- |
| 状态 | 字符串 | HTTP状态代码 |
| 带宽 | 整数 | 流的带宽 |
| 分 | 整数 | 流中的PTS时间 |
| ms_time | 整数 | 清单服务器生成跟踪网址的时间 |
| url | 字符串 | 重定向URL |
| header_user_agent | 字符串 | HTTP User-Agent标头 |
| header_dnt | 整数 | HTTP do-not-track头 |
| effective_remote_address | 字符串 | IPv4有效的远程地址 |
| remoteaddress | 字符串 | IPv4远程地址 |

>[!NOTE]
>
>后四个字段是可选的。

## 有用资源 {#helpful-resources}

* 请参阅完整的帮助文档，网址为 [Adobe Primetime学习与支持](https://helpx.adobe.com/support/primetime.html) 页面。
