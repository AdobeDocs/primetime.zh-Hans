---
title: 促进HLS播放器切换到故障切换/备份流
description: 如果Apple HLS栈栈无法检索主集的任何流，则它支持切换到故障转移/备份流。 对于Apple HLS设备，为了促进故障转移，您可以发送信号给manifest server ，将主控播放列表中标识的主流和故障转移流视为分离集（使用其自己的UUID）。
exl-id: 58c7a490-403f-41b2-bdbd-6f93e27083b0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---

# 促进HLS播放器切换到故障切换/备份流 {#facilitating-hls-player-switching-to-failover-backup-streams}

如果Apple HLS栈栈无法检索主集的任何流，则它支持切换到故障转移/备份流。 对于Apple HLS设备，为了促进故障转移，您可以发送信号给manifest server ，将主控播放列表中标识的主流和故障转移流视为分离集（使用其自己的UUID）。

为了便于在Apple HLS设备上切换到故障转移或备份流，您可以指定 `ptfailover` 参数BootstrapURL中的。 如果提供此参数，清单服务器将为每个故障转移集创建单独的播放会话（确定拼接的广告）。

## 详细信息

SSAI在您包括时如何处理HLS切换到故障切换/备份 `ptfailover=true` 在Bootstrap请求中：

* 当主控播放列表包含主播放集和备份集时：

   * 清单服务器使用为不同的故障转移集标识AV流URL `BANDWIDTH` AV流URL的属性和解析顺序。 它创建单独的内部播放会话（由单独的UUID标识），并创建指向清单服务器的流URL，其中不同UUID标识不同的播放会话。
   * 清单服务器使用匹配的标识不同故障转移集的I-Frame流URL `RESOLUTION` I-Frame流URL的属性和解析顺序。 SSAI使用标识关联的AV流的UUID用于指向SSAI的I-Frame流URL。
   * 对于此功能，清单服务器仅支持 `EXT-X-MEDIA` 主控播放列表中没有URI属性的组。
   * 清单服务器检测来自CDN的404错误响应，其中 `X-Object-Too-Old: true` 标头，并在将该响应发送到播放器时保留状态代码和标头。

* 前置广告仅添加到主集；在播放器切换到故障转移流时，故障转移集中会完全禁用前置广告，以避免任何错误和/或重复的前置广告。
