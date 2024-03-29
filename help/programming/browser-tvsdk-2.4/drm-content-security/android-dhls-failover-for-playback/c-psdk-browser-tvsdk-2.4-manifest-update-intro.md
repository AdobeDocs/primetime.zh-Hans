---
description: 浏览器TVSDK可以检测实时流主清单m3u8中的已更改播放信息，并在流播放时更新播放信息。 当配置文件在主清单中出现或消失时，浏览器TVSDK支持一组动态的比特率配置文件，包括更新之间不重叠的配置文件比特率。
title: 实时主清单更新
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---

# 实时主清单更新{#live-master-manifest-update}

浏览器TVSDK可以检测实时流主清单m3u8中的已更改播放信息，并在流播放时更新播放信息。 当配置文件在主清单中出现或消失时，浏览器TVSDK支持一组动态的比特率配置文件，包括更新之间不重叠的配置文件比特率。

支持以下功能：

* 配置文件计数（增加或减少）
* 配置文件比特率（重叠或不重叠）
* 具有相同（或不同）服务器URL的配置文件
* 任何故障转移结构

必须满足以下所有条件：

* 流是实时的。
* 时间和电子标签都会更改。
* 所有演绎版信息保持不变（但URL可能有所不同）。
* DRM访问信息保持不变。
* 将区段封装在误差较小的相同的PTS和帧边界周围。
