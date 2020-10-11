---
cloud: experience-cloud
product: adobe primetime
audience: end-user
user-guide-title: Primetime 动态 Ad Insertion 帮助
user-guide-description: Explains how to monetize content by inserting user-targeted dynamic ads on the server and engage audience with personalized ads.
translation-type: tm+mt
source-git-commit: 7d74e526dbc4c9f623d1ec30e4bc70d9318a89f9
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 2%

---


# Dynamic Ad Insertion Help {#ad-insertion}

+ [动态Ad Insertion概述](home.md)
+ PrimetimeAd Insertion{#get-started}
   + [概述](get-started-ptai.md)
   + [准备使用PrimetimeAd Insertion](setup-ptai.md)
   + [集成广告服务器](integrate-ad-server.md)
   + [集成CDN](integrate-cdn.md)
   + [在实时／线性流中使用广告插入](ad-insertion-live-linear-stream.md)
   + [将广告插入用于VOD](ad-insertion-vod.md)
   + [设置广告跟踪](set-up-ad-tracking.md)
+ [动态Ad Insertion发行说明](https://docs.adobe.com/content/help/en/primetime/release-notes/ptai/ptai-19x-release-notes.html)
+ [清单服务器调试工具](manifest-server-debugging-tool.md)

<!-- + [Server Side Ad Insertion debugging dashboard](ssai-debugging-dashboard.md)-->
+ 清单服务器API用于Ad Insertion {#manifest-server}
   + [清单服务器交互概述](msapi-topics/ms-overview.md)
   + Manifest Server入门 {#get-started}
      + [向清单服务器发送命令](msapi-topics/ms-getting-started/ms-sending-cmd.md)
      + [清单服务器查询参数](msapi-topics/ms-getting-started/ms-api-query-params.md)
   + 广告插入请求 {#ad-insert}
      + [广告插入请求](msapi-topics/ms-insert-ads/ms-ad-insert.md)
      + [按客户端和情况选择的查询参数](msapi-topics/ms-insert-ads/ms-api-query-param-situation.md)
      + [促进HLS播放器切换到故障转移／备份流](msapi-topics/ms-insert-ads/hls-switching-to-failover.md)
      + [多比特率流](msapi-topics/ms-insert-ads/ms-api-mbr-streams.md)
      + [部分广告中断插入](msapi-topics/ms-insert-ads/partial-ad-break-insetion.md)
      + [针对CRS广告投放的多个CDN支持](msapi-topics/ms-insert-ads/ms-api-multi-cdns-for-crs.md)
   + 替换VOD时间轴 {#replace-vod}
      + [对VOD的更改](msapi-topics/ms-changes-vod-timeline/ms-replace-vod-timeline.md)
      + [VOD时间轴格式](msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md)
      + [替换VOD时间轴](msapi-topics/ms-changes-vod-timeline/t-ms-replace-vod-timeline.md)
   + 广告效果跟踪 {#ad}
      + [广告跟踪](msapi-topics/ms-at-effectiveness/ms-at-overview.md)
      + [启用客户端广告跟踪](msapi-topics/ms-at-effectiveness/ms-enable-client-side-ad-tracking.md)
      + [非TVSDK客户端跟踪概述](msapi-topics/ms-at-effectiveness/notvsdk-csat-overview.md)
      + [用于播放器与清单服务器交互的API](msapi-topics/ms-at-effectiveness/notvsdk-csat-ms-interface.md)
      + [EXT-X-MARKER指令](msapi-topics/ms-at-effectiveness/ms-api-playlists.md)
   + [Cookie](msapi-topics/ms-cookies.md)
   + [支持WebVTT字幕](msapi-topics/ms-webvtt-captions.md)
   + 列表文件格式 {#list}
      + [文件格式](msapi-topics/ms-list-file-formats/ms-api-file-formats.md)
      + [用于请求变型清单播放列表的URL的JSON格式](msapi-topics/ms-list-file-formats/ms-json-m3u8.md)
      + [用于跟踪URL的JSON格式](msapi-topics/ms-list-file-formats/notvsdk-csat-sidecar.md)
      + [用于跟踪URL的VMAP格式](msapi-topics/ms-list-file-formats/notvsdk-csat-vmap.md)
   + [视频播放器要求](msapi-topics/ms-player-req.md)
+ Primetime Creative Repackaging Service {#crs}
   + [CRS概述](creative-repackaging-service/crs-overview.md)
   + [CRS的主要用途](creative-repackaging-service/jit-async-hls-conv.md)
   + [多CDN支持](creative-repackaging-service/multi-cdn-supportt.md)
   + [JIT重新打包的详细工作流](creative-repackaging-service/jit-repackage.md)
   + [使用CRS插入ID3定时元数据标记](creative-repackaging-service/inject-id3.md)
   + [重新打包API](creative-repackaging-service/api-repackage.md)
