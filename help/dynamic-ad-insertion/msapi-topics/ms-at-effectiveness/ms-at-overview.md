---
description: 大多数广告商需要一些关于广告的观看时间、观看时间以及观看成功程度的详细信息。 最有效的方法是让客户端播放器在播放广告时发送报告，但清单服务器也支持服务器端和混合广告跟踪。
seo-description: 大多数广告商需要一些关于广告的观看时间、观看时间以及观看成功程度的详细信息。 最有效的方法是让客户端播放器在播放广告时发送报告，但清单服务器也支持服务器端和混合广告跟踪。
seo-title: 广告跟踪
title: 广告跟踪
uuid: 184b8c36-5e51-42a7-b905-53f2b7b15e49
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9

---


# 广告跟踪 {#ad-tracking}

大多数广告商需要一些关于广告的观看时间、观看时间以及观看成功程度的详细信息。 最有效的方法是让客户端播放器在播放广告时发送报告，但清单服务器也支持服务器端和混合广告跟踪。

启用和跟踪时，客户端会指定以下方法之一：

* **客户端** ，服务器连同广告拼接的播放列表一起向客户端发送指定跟踪事件和URL的JSON、VMAP或清单内结构。 此方法符合Interactive Advertising Bureau(IAB)规范

* **服务器端** ，客户端不参与广告跟踪。 服务器会发送其能够发送的任何广告跟踪信息。 跟踪数据仅在服务器端计算，并且可能与客户端播放活动不匹配。 例如，如果最终用户不查看整个广告，则在传送区段后，服务器仍会考虑要播放的广告。

* **Hybrid** This as like client-side tracking, but the client send its reports to the manifest server, which this the reports their to the appriate URLs. 广告商会收到与客户端跟踪相同的信息。 此模式允许使用受限Internet访问运行的客户端。