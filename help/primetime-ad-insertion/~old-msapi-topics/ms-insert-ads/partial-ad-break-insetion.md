---
description: 部分广告时间插入(PABI)功能模仿电视体验，如果用户在中段广告时间加入实时流，则向用户显示中段广告，而不是前段广告或石板。
title: 部分广告时间插入
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# 部分广告时间插入 {#partial-ad-break-insertion}

部分广告时间插入(PABI)功能模仿电视体验，如果用户在中段广告时间加入实时流，则向用户显示中段广告，而不是前段广告或石板。

当广告服务器为实时流返回前置广告时，清单服务器将在实时点之前插入前置广告时间，并插入其TIMEOFFSET值指向前置广告时间开始的EXT-X-START标记。 此默认行为可确保在整个前置广告时间之前在实时点播放内容。 如果用户在实时点临近中置广告时间时加入流，则会在实时点处的中置广告时间之前向用户显示前置广告时间。

PABI功能指示清单服务器忽略前置广告时间，并将EXT-X-START：TIMEOFFSET值设置为实时点呈现的中置广告的开头。 这可确保用户无需查看前置广告时间，即可查看当前在实时点播放的整个中置广告。

>[!NOTE]
>
>此功能仅适用于实时流。 默认情况下，清单服务器会将前置广告时间插入VOD播放列表顶部。

>[!NOTE]
>
>要启用PABI，您需要指定 [query_params](/help/primetime-ad-insertion/~old-msapi-topics/ms-getting-started/ms-api-query-params.md) 在引导URL中。

>[!NOTE]
>
>此 [EXT-X-START](https://tools.ietf.org/html/rfc8216#section-4.3.5.2) 是一个标准HLS标记，指示播放列表中的首选起点。

## Recommendations {#section_4CF0733B14504F2A99690310B9F3B130}

* 使用客户端跟踪，因为客户端对跟踪信标的触发具有更大的控制力。
* 仅当播放器支持EXT-X-START时，部分广告时间才应用于服务器端跟踪模式。