---
title: 促进HLS播放器切换到故障切换/备份流
description: 如果无法检索主集的任何流，Apple HLS栈栈支持切换到故障切换/备份流。 对于Apple HLS设备，为了促进故障转移，您可以发出信号通知清单服务器，将主播放列表中标识的主流和故障转移流视为分离集（具有它们自己的UUID）。
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---

# 促进HLS播放器切换到故障切换/备份流 {#facilitating-hls-player-switching-to-failover-backup-streams}

如果无法检索主集的任何流，Apple HLS栈栈支持切换到故障切换/备份流。 对于Apple HLS设备，为了促进故障转移，您可以发出信号通知清单服务器，将主播放列表中标识的主流和故障转移流视为分离集（具有它们自己的UUID）。

为了便于在Apple HLS设备上切换到故障转移或备份流，您可以指定 `ptfailover` Bootstrap参数。 如果提供此参数，清单服务器将为每个故障转移集创建单独的播放会话（用于决定拼接的广告）。

## 详细信息

SSAI在您包括时如何处理HLS切换到故障切换/备份 `ptfailover=true` 在Bootstrap请求中：

* 当主播放列表包含主播放集和备份集时：

   * 清单服务器使用为不同的故障转移集标识AV流URL `BANDWIDTH` 属性和AV流URL的解析顺序。 它创建单独的内部播放会话（由单独的UUID标识），并创建指向清单服务器的流URL，这些UUID可标识不同的播放会话。
   * 清单服务器使用匹配为不同的故障转移集标识I-Frame流URL `RESOLUTION` 属性和I帧流URL的解析顺序。 SSAI使用用于标识指向SSAI的I-Frame流URL的关联AV流的UUID。
   * 对于此功能，清单服务器仅支持 `EXT-X-MEDIA` 主播放列表中没有URI属性的组。
   * 清单服务器检测来自CDN的404错误响应，该响应具有 `X-Object-Too-Old: true` 标头，并在向播放器发送响应时保留状态代码和标头。

* 前段广告仅添加到主集；在播放器切换到故障转移流时，会在故障转移集中完全禁用前段广告，以避免任何错误和/或重复的前段广告。
