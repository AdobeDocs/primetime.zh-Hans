---
description: 部分广告中断插入(PABI)功能模仿电视的体验，在这种体验中，如果用户在中间广告中断内加入实时流，则用户将显示中间广告，而不是前广告或板片广告。
seo-description: 部分广告中断插入(PABI)功能模仿电视的体验，在这种体验中，如果用户在中间广告中断内加入实时流，则用户将显示中间广告，而不是前广告或板片广告。
seo-title: 部分广告中断插入
title: 部分广告中断插入
uuid: a0c1ae34-0f8d-4401-97fe-45a2ea40d08d
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---


# 部分广告中断插入{#partial-ad-break-insertion}

部分广告中断插入(PABI)功能模仿电视的体验，在这种体验中，如果用户在中间广告中断内加入实时流，则用户将显示中间广告，而不是前广告或板片广告。

当广告服务器返回实时流的预卷广告时，清单服务器将在实时点之前插入预卷广告中断，并插入EXT-X-开始标签，其TIMEOFFSET值指向预卷广告中断的开始。 此默认行为确保在实时点上的内容播放之前播放整个前置广告。 如果用户在实时点接近中间广告中断时加入流，则用户将在实时点的中间广告中断之前显示前广告中断。

PABI功能指示清单服务器忽略前滚和中断，并将EXT-X-开始:TIMEOFFSET值设置为中间卷的开始，并在实时点显示。 这可确保用户看到当前在实时点播放的整个中间广告，而无需视图前期广告中断。

>[!NOTE]
>
>此功能仅对实时流可用。 默认情况下，清单服务器将前置和中断插入VOD播放列表的顶部。

>[!NOTE]
>
>要启用PABI，您需要在引导URL中指定[查询params](../../msapi-topics/ms-getting-started/ms-api-query-params.md)。

>[!NOTE]
>
>[EXT-X-开始](https://tools.ietf.org/html/rfc8216#section-4.3.5.2)是标准HLS标记，它指示播放列表中的首选起始点。

## Recommendations{#section_4CF0733B14504F2A99690310B9F3B130}

* 使用客户端跟踪，因为客户端对触发跟踪信标有更多控制。
* 如果播放器支持EXT-X-开始，部分广告中断仅应用于服务器端跟踪模式。