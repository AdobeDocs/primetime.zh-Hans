---
description: 部分广告中断插入(PABI)功能模仿电视体验，如果用户在中间广告中断内加入实时流，则用户将显示中间广告，而不是前广告或板岩广告。
seo-description: 部分广告中断插入(PABI)功能模仿电视体验，如果用户在中间广告中断内加入实时流，则用户将显示中间广告，而不是前广告或板岩广告。
seo-title: 部分广告中断插入
title: 部分广告中断插入
uuid: a0c1ae34-0f8d-4401-97fe-45a2ea40d08d
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9

---


# 部分广告中断插入 {#partial-ad-break-insertion}

部分广告中断插入(PABI)功能模仿电视体验，如果用户在中间广告中断内加入实时流，则用户将显示中间广告，而不是前广告或板岩广告。

当广告服务器返回实时流的预卷广告时，清单服务器将在实时点之前插入预卷广告中断，并插入EXT-X-START标签，其TIMEOFFSET值指向预卷广告中断的开始。 此默认行为可确保在实时点的内容之前播放整个前置广告中断。 如果用户在实时点接近中间广告中断时加入流，则用户将在实时点显示中间广告中断之前的前广告中断。

PABI功能指示清单服务器忽略前置和中断，并将EXT-X-START:TIMEOFFSET值设置为中间卷的开头，并在实时点显示。 这可确保用户无需查看前置广告中断即可查看当前在实时点播放的整个中间广告。

>[!NOTE]
>
>此功能仅对实时流可用。 默认情况下，清单服务器将前置和中断插入VOD播放列表之上。

>[!NOTE]
>
>要启用PABI，您需要在引导URL [中指定query_params](../../msapi-topics/ms-getting-started/ms-api-query-params.md) 。

>[!NOTE]
>
>[EXT-X-START](https://tools.ietf.org/html/rfc8216#section-4.3.5.2) 是标准HLS标签，它指示播放列表中的首选起始点。

## 建议 {#section_4CF0733B14504F2A99690310B9F3B130}

* 使用客户端跟踪，因为客户端对跟踪信标的触发具有更多控制权。
* 部分广告中断仅应与服务器端跟踪模式一起使用（如果播放器支持EXT-X-START）。