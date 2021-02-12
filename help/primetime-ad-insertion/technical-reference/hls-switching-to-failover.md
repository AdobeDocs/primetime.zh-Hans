---
title: 促进HLS播放器切换到故障转移／备份流
description: 如果Apple HLS堆栈无法检索主集的任何流，则它支持切换到故障转移／备份流。 对于Apple HLS设备，为了便于故障转移，您可以发出信号通知清单服务器将主控播放列表中标识的主流和故障转移流视为不连接集（使用它们自己的UUID）。
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---


# 促进HLS播放器切换到故障转移／备份流{#facilitating-hls-player-switching-to-failover-backup-streams}

如果Apple HLS堆栈无法检索主集的任何流，则它支持切换到故障转移／备份流。 对于Apple HLS设备，为了便于故障转移，您可以发出信号通知清单服务器将主控播放列表中标识的主流和故障转移流视为不连接集（使用它们自己的UUID）。

为便于切换到Apple HLS设备上的故障转移或备份流，可在BootstrapURL中指定`ptfailover`参数。 如果您提供此参数，清单服务器将为每个故障转移集创建单独的播放会话（确定拼接广告）。

## 详细信息

当您在Bootstrap请求中包含`ptfailover=true`时，SSAI如何处理HLS切换到故障转移／备份：

* 当主控的播放列表包含主播放列表和备份集时：

   * 清单服务器使用`BANDWIDTH`属性和AV流URL的解析顺序来标识不同故障转移集的AV流URL。 它创建单独的内部播放会话（由单独的UUID标识），并创建指向清单服务器的流URL，这些清单服务器具有标识不同播放会话的不同UUID。
   * 清单服务器使用匹配的`RESOLUTION`属性和I帧流URL的解析顺序为不同故障转移集标识I帧流URL。 SSAI使用UUID标识指向SSAI的I帧流URL的关联AV流。
   * 对于此功能，清单服务器仅支持主控播放列表中没有URI属性的`EXT-X-MEDIA`组。
   * 清单服务器检测来自具有`X-Object-Too-Old: true`头的CDN的404错误响应，并在将该响应发送到播放器时保留状态代码和头。

* 预卷广告只添加到主集合；它们在故障转移集中被完全禁用，以避免在播放器切换到故障转移流时出现任何错误和／或重复的预卷广告。
