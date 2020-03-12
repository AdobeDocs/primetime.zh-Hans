---
title: 清单服务器调试工具
seo-title: 清单服务器调试工具
description: 清单服务器调试工具
seo-description: 清单服务器调试工具
uuid: 0b4f06f5-4b1f-4f88-980a-5b4df28e0094
products: SG_PRIMETIME
topic-tags: ad-insertion
discoiquuid: 00b49659-ce56-4b5c-87cd-c357a0936641
donotlocalize: false
moreHelpPaths: /content/help/en/primetime/morehelp/ad-insertion;/content/help/en/primetime/morehelp/ad-insertion
pagecreatedat: en
pagelayout: video
sidecolumn: left
translation-type: tm+mt
source-git-commit: b77f4988103b68d0ce8926407d2ccb2e0c68e322

---


# 清单服务器调试工具 {#manifest-server-debugging-tool}

## 调试工具概述 {#overview-of-debugging-tool}

该调试工具使发行商能够通过检查清单服务器在HTTP头中返回的调试信息来调查可能代价高昂的广告插入问题，或者，当需要更详细的信息时，检查事实后的会话日志。 Akamai等Adobe合作伙伴可以使用该工具调试与Primetime广告决策的集成。

该工具支持在任何主清单服务器和跟踪配置中调试和插入问题：

* 使用基于TVSDK的播放器进行客户端跟踪。
* 使用不基于TVSDK的播放器进行客户端跟踪。
* 服务器端跟踪。

要支持所有这些情况，该工具不需要或使用播放器发布者代码。

启动清单服务器会话时，可以在请求URL上设置一个参数，要求它记录调试信息。 使用该参数的不同值，您还可以要求清单服务器在HTTP头中返回指定的调试信息，但头只能包含有限数量的信息。 您可以从Adobe获取凭据以访问完整的日志文件，清单服务器会定期（例如，每小时）保存到存档服务器上。 拥有该服务器的凭据后，您可以随时直接访问它。

<!-- You can also see the [server side event tracking captured in the SSAI dashboard](ssai-debugging-dashboard.md).-->

## 调试工具选项 {#debugging-tool-options}

调用调试工具时，有几个选项可用于确定清单服务器在HTTP头中返回的信息。 这些选项不会影响清单服务器在日志文件中放置的内容。

### 指定ptdebug {#specifying-ptdebug}

在为清单服务器会话启动调试日志记录时，可以向请求URL添加ptdebug参数，以指定清单服务器在HTTP头中返回的信息的以下选项：

* ptdebug=true除记录之外的所 `TRACE_HTTP_HEADER` 有记录和大 `call/response data` 多数记 `TRACE_AD_CALL` 录。
* ptdebug=AdCall Only TRACE_AD_*type* （例如，TRACE_AD_CALL）记录。
* ptdebug=仅标题TRACE_HTTP_HEADER记录。

这些选项不会影响清单服务器在日志文件中放置的内容。 您无法控制这一点，但日志文件是文本文件，因此您可以应用各种工具提取您感兴趣的信息并重新设置其格式。

以下是返回的HTTP头示例 `ptdebug=Header`。 某些十六进制数字的长字符串将替换为 `. . .` 清晰性。

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

每个日志记录都有一个类型和一组字段，其中一些字段可能是可选的。 在记录类型之前的所有记录的字段都相同。 它们提供有关会话的时间戳和信息。 记录类型标识所记录活动的类型，后续字段提供有关所记录活动的信息。

日志记录的结构如下：

`datetime request_id session_id zone_id record_type` 其他 *字段。*

| 字段 | 类型 | 说明 |
|--- |--- |--- |
| datetime | 字符串 | 时间戳 |
| request_id | 字符串 | 清单服务器使用的请求ID（unix时间戳） |
| session_id | 字符串 | 清单服务器使用的会话ID |
| zone_id | 整数 | 区域ID |
| record_type | 字符串 | 正在记录的活动类型 |
| 其他字段 | *** | 取决于事件的类型 |

### TRACE_REQUEST_INFO记录 {#trace-request-info-records}

此类型的记录记录HTTP请求的结果。 TRACE_REQUEST_INFO之外的字段按表中显示的顺序显示，以选项卡分隔。

| 字段 | 类型 | 说明 |
|--- |--- |--- |
| 状态 | 字符串 | 返回的HTTP状态代码 |
| request_method | 字符串 | HTTP方法（GET或POST） |
| request_uri | 字符串 | HTTP请求URI（无主机） |
| request_length | 整数 | 请求长度（字节） |
| response_length | 整数 | 响应长度（字节） |
| δ | 整数 | 处理请求的时间（毫秒） |
| module_type | 字符串 | 变体、流或VOD |
| remote_address_aud_client_ip | 字符串 | （请参阅附注） |
| remote_address_x_fwd_for_hdr_key | 字符串 | （请参阅附注） |
| remote_host_port | 字符串 | （请参阅附注） |

>[!NOTE]
>
>最后三个字段为可选字段。

示例：

```
1427263800524 6495aafc-3f34-4047-ad36-350d4f056eb4 189938
TRACE_REQUEST_INFO 301 GET /auditude/variant/pubAsset/aHR0cDov. . ..m3u8
?u=cecebae72a919de350b9ac52602623f3&z=189938&ptcueformat=turner& sid =yk-cnnlive-003 &ptdebug=true 0 0 0 Variant 111.22.3.44 111.22.3.45 127.0.0.1:46383
```

### TRACE_HTTP_HEADER记录 {#trace-http-header-records}

在清单服务器与客户端、广告服务器或内容服务器之间的HTTP调用期间交换的此类记录日志HTTP头。 超出TRACE_HTTP_HEADER的字段按表中显示的顺序显示，以选项卡分隔。

| 字段 | 类型 | 说明 |
|--- |--- |--- |
| request_type | 字符串 | 请求类型（MAIN或UNKNOWN） |
| request_response | 字符串 | 响应标题（请求或响应） |
| header_name | 字符串 | HTTP头名称 |
| header_value | 字符串 | Base64编码的HTTP头值 |

>[!NOTE]
>
>request_type和header_value字段是可选字段。

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

### TRACE_AD_CALL记录 {#trace-ad-call-records}

此类型的记录记录清单服务器和请求的结果。 TRACE_AD_CALL之外的字段按表中显示的顺序显示，以选项卡分隔。

| 字段 | 类型 | 说明 |
|--- |--- |--- |
| 状态 | 字符串 | 返回的HTTP状态代码 |
| request_duration | 整数 | 从请求到响应的时间（毫秒） |
| ad_server_query_url | 字符串 | 广告调用的URL，包括查询参数 |
| ad_system_id | 字符串 | 广告系统，从广告服务器响应（如果未指定，则为Auditude） |
| avail_id | 字符串 | 可用的ID，来自内容清单文件中的广告提示（对于VOD，为N/A） |
| avail_duration | 数字 | 可用的持续时间（秒），从内容清单文件中的广告提示（VOD为N/A） |
| ad_server_response | 字符串 | 来自广告服务器的Base64编码响应 |

示例：

```
2015-03-25T06:13:31.271Z 14272. . . 189938 TRACE_AD_CALL
200 8 https://ad.stg2.auditude.com/adserver/a?cip=0.0.0.0&g=1000012&of=1.5 &ptcueformat=turner&ptdebug=true&tl=l,150,30,m&tm=63&u=ceceb. . . Auditude IvpIyC. . . 150 PD94bWw. . .
```

### TRACE_AD_INSERT、TRACE_AD_RESOLVE和TRACE_AD_REDIRECT记录 {#trace-ad-insert-trace-ad-resolve-and-trace-ad-redirect-records}

此类型的记录将记录由记录类型指示的广告请求的结果。 超出记录类型的字段以表格中显示的顺序显示，以制表符分隔。

| 字段 | 类型 | 说明 |
|--- |--- |--- |
| 状态 | 字符串 | 返回的HTTP状态代码 |
| avail_id | 字符串 | 可用的ID，来自内容清单文件（实时）中的ad cue或来自清单服务器(VOD) |
| ad_type | 字符串 | 广告类型（直接或重定向） |
| ad_duration | 整数 | 广告持续时间（秒），来自广告服务器响应 |
| ad_content_url | 字符串 | 广告的清单文件的URL，来自广告服务器响应 |
| ad_content_url_actual | 字符串 | 已插入广告的清单文件的URL。 对于TRACE_AD_REDIRECT为空。 |
| ad_system_id | 字符串 | 广告系统，从广告服务器响应（如果未指定，则为Auditude） |
| ad_id | 字符串 | 广告的ID，来自广告服务器响应 |
| creative_id | 字符串 | 来自广告节点、来自广告服务器响应的创意ID |
| ad_call_id | 字符串 | 未使用。 保留供将来使用。 |
| δ | 整数 | 此事件所花费的时间（毫秒） |
| misc | 字符串 | 跳过广告的原因 |

>[!NOTE]
>
>ad_content_url_actual、ad_call_id和misc字段是可选字段。

对于TRACE_AD_RESOLVE和TRACE_AD_INSERT,ad_content_url_actual字段中的URL用于转码广告（如果有）。 否则，对于TRACE_AD_RESOLVE，该字段为空，对于TRACE_AD_INSERT，该字段与ad_content_url相同。

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

此类记录将记录清单服务器和请求的结果。 TRACE_TRACKING_URL之外的字段按表中显示的顺序显示，以选项卡分隔。

| 字段 | 类型 | 说明 |
|--- |--- |--- |
| pts | 数字 | 程序时间戳。 在视频中调用URL的时间。 |
| ad_system | 字符串 | 广告系统（auditude或自由轮） |
| url | 字符串 | URL已pinged |
| 状态 | 字符串 | ping返回的HTTP状态 |

示例：

```
2015-06-04T23:24:42.000-0700    1426742736208     3086f5cd . . .    12345    TRACE_TRACKING_URL
    0.000000    ExampleSystem    https://localhost/index.php?stream:test#8.1433485415;
    sid:3086f5cd . . .;pts:0    200
```

### TRACE_TRONDING_NO_MEDIA_TO_TRANSCODE记录 {#trace-transcoding-no-media-to-transcode-records}

此类型的记录记录缺少广告创意。 表中显示唯一超出TRACE_TRONDING_NO_MEDIA_TO_TRANSCODE的字段。

| 字段 | 类型 | 说明 |
|--- |--- |--- |
| ad_id | 字符串 | 完全限定的广 `(FQ_AD_ID: Q_AD_ID[;Q_AD_ID[;Q_AD_ID...]`告ID] Q_AD_ID: `PROTOCOL:AD_SYSTEM:AD_ID[:CREATIVE_ID[:MEDIA_ID]`]协议：AUDITUDE, VAST) |

### TRACE_TROCNDING_REQUESTED记录 {#trace-transcoding-requested-records}

此类记录记录记录清单服务器发送到CRS的转码请求的结果。 超出TRACE_CRONDING_REQUESTED的字段按表中显示的顺序显示，以选项卡分隔。

| 字段 | 类型 | 说明 |
|--- |--- |--- |
| ad_id | 字符串 | 完全限定的广告ID |
| ad_manifest_url | 字符串 | 广告的清单文件的URL，来自广告服务器响应 |
| creative_type | 字符串 | 媒体类型 |
| 标志 | 字符串 | ID3指示转码请求是否包括添加ID3标记的请求 |
| target_duration | 字符串 | 转码创意的目标持续时间（秒） |

### TRACE_TRACKING_REQUEST记录 {#trace-tracking-request-records}

此类型的记录指示执行服务器端跟踪的请求。 TRACE_TRACKING_REQUEST之外的字段按表中显示的顺序显示，以选项卡分隔。

| 字段 | 类型 | 说明 |
|--- |--- |--- |
| tracking_url_count | 整数 | 跟踪URL的数量 |
| 开始 | 浮动 | PTS片段开始时间（秒，精确到毫秒） |
| end | 浮动 | PTS片段结束时间（秒，精确到毫秒） |

### TRACE_TRACKING_REQUEST_URL记录 {#trace-tracking-request-url-records}

此类记录提供了用于服务器端跟踪的跟踪URL。 超出TRACE_TRACKING_REQUEST_URL的字段按表中显示的顺序显示，以选项卡分隔。

| 字段 | 类型 | 说明 |
|--- |--- |--- |
| 时间戳 | 浮动 | 播放会话中ping跟踪URL的时间（秒，精度为。001） |
| ad_system | 字符串 | 广告系统（例如，auditude） |
| url | 字符串 | 要ping的URL |

### TRACE_WEBVTT_REQUEST记录 {#trace-webvtt-request-records}

此类型日志的记录请求清单服务器为WEBVTT字幕发出的请求。 TRACE_WEBVTT_REQUEST之外的字段按表中显示的顺序显示，以选项卡分隔。

| 字段 | 类型 | 说明 |
|--- |--- |--- |
| 状态 | 字符串 | 返回的HTTP状态代码 |
| vtt_uri | 字符串 | 请求的URL |
| 开始 | 浮动 | 分割开始时间（秒，精确到毫秒） |
| end | 浮动 | 分段结束时间（秒，精确到毫秒） |

### TRACE_WEBVTT_RESPONSE记录 {#trace-webvtt-response-records}

将记录 ``of ``日志日志 ``type ``记录到服务 ``responses ``器中，以 ``manifest ``便将 ``sends ``此标题记 ``clients ``录 `` `answer` ````requests ```for```WEBVTT ``到此标题中。 TRACE_WEBVTT_RESPONSE &#39;&#39;之外的字段按表中显示的顺序(以分隔的选项卡 `by`显示)。

| 字段 | 类型 | 说明 |
|--- |--- |--- |
| 状态 | 字符串 | 返回的HTTP状态代码 |
| 响应 | 字符串 | 发送到客户端的Base64编码响应 |

### TRACE_WEBVTT_SOURCE记录 {#trace-webvtt-source-records}

此类型的记录记录对清单服务器发出的WEBVTT题注的请求做出响应。 TRACE_WEBVTT_SOURCE之外的字段按表中显示的顺序显示，以选项卡分隔。

| 字段 | 类型 | 说明 |
|--- |--- |--- |
| 状态 | 字符串 | 返回的HTTP状态代码 |
| 源 | 字符串 | 基本64编码的原始VTT内容 |


### TRACE_MISC记录 {#trace-misc-records}

此类记录使清单服务器能够记录在收录广告时未计划的事件和信息。 TRACE_MISC之外的字段由消息字符串组成。 可能显示的消息包括：

* 已忽略广告：AdPlacement `[adManifestURL=https://cdn2.auditude.com/assets/3p/v2/8c/2b/8c2bb. . . .m3u8, durationSeconds=15.0, ignore=false, redirectAd=false, priority=1]`
* AdPlacement adManifestURL=*adManifestURL*, durationSeconds=*seconds*, ignore=ignore *, redirectAd=****redirectAdPriority=priorityPriority*
* 广告投放返回null。
* 广告拼接成功。
* 广告呼叫失败：错 *误消息*。
* 添加用户代理以获取原始清单：用 *户代理*。
* 添加Cookie以获取原始清单： [cookie]
* 请求的URL *错误消息*。 （无法解析变体URL）
* 调用的url:URL获 *得退回：响应代码*。 （实时URL）
* 调用的url:URL返 *回代码：响应代码*。 (VOD URL)
* 解决广告时发现冲突：中间辊起始端或中间辊端之一位于中间辊(VOD)中包含的预辊或预辊内。
* 检测到URI的处理函数引发的未处理异常：请 *求URL*。
* 已完成变型清单的生成。 （变体）
* 已完成变型清单的生成。
* 处理VAST重定向*重定向URL *错误：错 *误消息*。
* 无法获取广告的播放列表以获取 *广告清单URL*。
* 无法生成目标清单。 (HLSManifestResolver)
* 无法解析第一个广告调用响应：错 *误消息*。
* 无法处理*GET|POST *路径请求：请 *求URL*。 （实时／视频点播）
* 无法处理Live Manifest请求：请 *求URL*。 （实时）
* 无法返回变体清单：错 *误消息*。
* 无法验证组ID:组 *ID*。
* 获取原始清单：内 *容URL*。 （实时）
* 遵循VAST重定向：重 *定向URL*。
* 找到空的可用内容。 (VOD)
* 找到*数量*广告。 (VOD)
* 收到HTTP请求。 （第一条消息）
* 忽略广告，因为广告响应持续时间（*广告响应持续时间*秒）与实际广告持续时间（*实际持续时间*秒）之间的差异大于限制。 (HLSManifestResolver)
* 将忽略未提供ID值的可用值。 (GroupAdResolver.java)
* 忽略提供无效时间值的有用值：*time *for availId = *avail ID*。
* 忽略提供无效持续时间值的有用值：*duration *for availId = *avail ID*。
* 初始化新会话。 （变体）
* HTTP方法无效。 它必须是GET。 (VOD)
* HTTP方法无效。 跟踪请求必须是GET。 （实时）
* 请求的URL *错误消息无效*。 （变体）
* 组无效。 (HLSManifestResolver)
* 请求无效。 题注不是有效的跟踪请求。 (VOD)
* 请求无效。 题注请求必须在会话建立后发出。 (VOD)
* 请求无效。 必须在会话建立后发出跟踪请求。 (VOD)
* 过载组ID的服务器实例无效：组 *ID*。 （实时）
* 已达到VAST重定向的限 *制——数*。
* 拨打广告电话：广 *告呼叫URL*。
* 找不到以下对象的清单：内 *容URL*。 （实时）
* 找不到适用ID的匹配用项：可 *用ID*。 (HLSManifestResolver)
* 未找到播放会话。 (HLSManifestResolver)
* 处理清单内容URL *的VOD请求*。
* 正在处理变体。
* 处理清单内容URL的 *题注请求*。
* 正在处理跟踪请求。 (VOD)
* 重定向广告响应为空。 (VASTStAX)
* 请求： *URL*。
* 返回GET请求的错误响应，因为未找到播放会话。 (VOD)
* 由于内部服务器错误，为GET请求返回错误响应。
* 为指定无效资产的GET请求返回错误响应： *广告请求ID*。 (VOD)
* 为指定无效或空组ID的GET请求返回错误响应：组 *ID*。 (VOD)
* 为指定无效跟踪位置值的GET请求返回错误响应。 (VOD)
* 对语法无效的GET请求返回错误响应- *请求URL*。 （实时／视频点播）
* 使用不支持的HTTP方法返回请求的错误响应： *获取|发布*。 （实时／视频点播）
* 从缓存返回清单。 (VOD)
* 服务器过载。 无需广告拼合请求即可继续。 （变体）
* 开始生成目标清单。 (HLSManifestResolver)
* 开始从以下位置生成变体清单：内 *容URL*。 （变体）
* 开始将广告拼合到清单中。 (VODHLSResolver)
* 尝试在 *HH:MM:SS处缝合广告*:AdPlacement [adManifestURL=*ad Manifest URL*, durationSeconds=*seconds* ignore, redirectAd *=redirectAdPriority=redirectPriority*****=redirectPriorityOrity. (HLSManifestResolver)
* 由于时间轴无效，无法获取广告——返回不含广告的内容。 (VOD)
* 无法获取广告——返回不含广告的内容。 (VOD)
* 无法获取广告查询，并且未提供内容URL。 (VOD)
* 收到有效的URL。 （VOD/变体）
* 找不到变体M3U8。 （变体）

### TRACE_TRACKING_URL记录 {#trace-tracking-url-records-1}

清单服务器在服务器端跟踪工作流程中调用跟踪URL后生成此类记录。 TRACE_TRACKING_URL之外的字段按表中显示的顺序显示，以选项卡分隔。

| 字段 | 类型 | 说明 |
|--- |--- |--- |
| pts | 数字 | 流中的PTS时间 |
| ad_system | 字符串 | 广告的广告系统（auditude或自由轮） |
| url | 字符串 | URL已pinged |
| 状态 | 字符串 | HTTP状态代码 |

### TRACE_PLAYBACK_PROGRESS记录 {#trace-playback-progress-records}

清单服务器在服务器端跟踪工作流期间接收关于回放进度的信号时生成这种记录。 超出TRACE_PLAYBACK_PROGRESS的字段按表中显示的顺序显示，以选项卡分隔。

| 字段 | 类型 | 说明 |
|--- |--- |--- |
| 状态 | 字符串 | HTTP状态代码 |
| 带宽 | 整数 | 流的带宽 |
| pts | 整数 | 流中的PTS时间 |
| ms_time | 整数 | 清单服务器生成跟踪URL的时间 |
| url | 字符串 | 重定向URL |
| header_user_agent | 字符串 | HTTP用户代理头 |
| header_dnt | 整数 | HTTP do-not-track头 |
| effective_remote_address | 字符串 | IPv4有效远程地址 |
| remote_address | 字符串 | IPv4远程地址 |

>[!NOTE]
>
>最后四个字段是可选的。

## 实用资源 {#helpful-resources}

* 请参阅 [Adobe Primetime学习和支持页面上的完整帮助文档](https://helpx.adobe.com/support/primetime.html) 。
