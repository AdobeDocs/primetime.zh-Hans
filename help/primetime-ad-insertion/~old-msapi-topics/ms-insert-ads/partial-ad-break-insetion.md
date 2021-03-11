---
description: “部分广告中断插入”(PABI)功能模仿电视的体验，在这种体验中，如果用户在中间广告时段内加入实时流，则用户将显示中间广告，而不是前置广告或插图。
title: 部分广告中断插入
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# 部分广告中断插入{#partial-ad-break-insertion}

“部分广告中断插入”(PABI)功能模仿电视的体验，在这种体验中，如果用户在中间广告时段内加入实时流，则用户将显示中间广告，而不是前置广告或插图。

当广告服务器返回实时流的前滚广告时，清单服务器将在实时点之前插入前滚广告中断，并插入EXT-X-开始标签，其TIMEOFFSET值指向前滚广告中断的开始。 此默认行为确保在实时点上的内容之前播放整个前滚广告片段。 如果用户在实况点附近加入流，则在实况点前向用户显示中间广告中断。

PABI功能指示清单服务器忽略前滚和中断，并将EXT-X-开始:TIMEOFFSET值设置为中间卷的开头，该中间卷在实时点出现。 这可确保用户无需视图前置广告中断即可看到整个中间广告当前在实时点播放。

>[!NOTE]
>
>此功能仅对实时流可用。 默认情况下，清单服务器将前置和中断插入VOD播放列表之上。

>[!NOTE]
>
>要启用PABI，您需要在引导URL中指定[查询_params](/help/primetime-ad-insertion/~old-msapi-topics/ms-getting-started/ms-api-query-params.md)。

>[!NOTE]
>
>[EXT-X-开始](https://tools.ietf.org/html/rfc8216#section-4.3.5.2)是标准HLS标记，指示播放列表中的首选起始点。

## Recommendations {#section_4CF0733B14504F2A99690310B9F3B130}

* 使用客户端跟踪，因为客户端对触发跟踪信标有更多控制。
* 如果播放器支持EXT-X-开始，则部分广告分段仅应与服务器端跟踪模式一起使用。