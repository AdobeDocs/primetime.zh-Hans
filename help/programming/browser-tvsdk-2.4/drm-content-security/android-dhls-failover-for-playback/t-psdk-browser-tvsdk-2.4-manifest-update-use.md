---
description: 您可以打开此功能并检查相关事件。
seo-description: 您可以打开此功能并检查相关事件。
seo-title: 使用实时主清单更新
title: 使用实时主清单更新
uuid: 4ec665ab-b7ce-4a45-a251-13a07eb4d789
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 使用实时主清单更新{#use-live-master-manifest-update}

您可以打开此功能并检查相关事件。

1. 要打开实时主清单更新，请通过设置属性来设置更新频率(以分钟为单 `NetworkConfiguration.masterUpdateInterval` 位)。
1. （可选）通过侦听事件来跟踪成功的清单 `MediaPlayerItemEvent.MASTER_UPDATED` 更新。
