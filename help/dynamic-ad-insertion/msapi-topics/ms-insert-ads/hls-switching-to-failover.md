---
description: 如果Apple HLS堆栈无法检索主集的任何流，则支持切换到故障转移／备份流。 对于Apple HLS设备，为了便于故障转移，可以发出信号，指示清单服务器将主播放列表中标识的主流和故障转移流视为断开连接的集（使用它们自己的UUID）。
seo-description: 如果Apple HLS堆栈无法检索主集的任何流，则支持切换到故障转移／备份流。 对于Apple HLS设备，为了便于故障转移，可以发出信号，指示清单服务器将主播放列表中标识的主流和故障转移流视为断开连接的集（使用它们自己的UUID）。
seo-title: 促进HLS播放器切换到故障转移／备份流
title: 促进HLS播放器切换到故障转移／备份流
uuid: 2fea8a51-e4cb-4fc9-82d5-6305a1d96603
translation-type: tm+mt
source-git-commit: 6863b63c7fa0068c3c5060fb946515c6cc5e3bff

---


# 促进HLS播放器切换到故障转移／备份流 {#facilitating-hls-player-switching-to-failover-backup-streams}

如果Apple HLS堆栈无法检索主集的任何流，则支持切换到故障转移／备份流。 对于Apple HLS设备，为了便于故障转移，可以发出信号，指示清单服务器将主播放列表中标识的主流和故障转移流视为断开连接的集（使用它们自己的UUID）。

为便于切换到Apple HLS设备上的故障转移或备份流，可在Bootstrap URL `ptfailover` 中指定该参数。 如果您提供此参数，清单服务器将为每个故障转移集创建单独的播放会话（确定拼接的广告）。

## 详细信息

在Bootstrap请求中包含SSAI时，SSAI如何处理HLS切换到故 `ptfailover=true` 障转移／备份：

* 当主播放列表包含主播放列表和备份集时：

   * 清单服务器使用AV流URL的属性和解析顺序来标识 `BANDWIDTH` 不同故障转移集的AV流URL。 它创建单独的内部播放会话（由单独的UUID标识），并创建指向清单服务器的流URL，其中不同的UUID标识不同的播放会话。
   * 清单服务器使用匹配属性和I帧流URL的解析顺序标识不 `RESOLUTION` 同故障转移集的I帧流URL。 SSAI使用UUID标识指向SSAI的I帧流URL的关联AV流。
   * 对于此功能，清单服务器仅支持主播放 `EXT-X-MEDIA` 列表中没有URI属性的组。
   * 清单服务器检测来自CDN的带头404错误响应，并在将该响应发送到播放器时保留状 `X-Object-Too-Old: true` 态代码和头。

* 预卷广告只添加到主集合；它们在故障转移集中被完全禁用，以避免在播放器切换到故障转移流时出现任何错误和／或重复的预卷广告。

