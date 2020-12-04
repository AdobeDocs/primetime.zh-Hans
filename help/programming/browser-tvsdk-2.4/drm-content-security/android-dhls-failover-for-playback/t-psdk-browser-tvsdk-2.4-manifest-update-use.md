---
description: 您可以打开此功能并检查相关事件。
seo-description: 您可以打开此功能并检查相关事件。
seo-title: 使用实时主控清单更新
title: 使用实时主控清单更新
uuid: 4ec665ab-b7ce-4a45-a251-13a07eb4d789
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 0%

---


# 使用实时主控清单更新{#use-live-master-manifest-update}

您可以打开此功能并检查相关事件。

1. 要打开实时主控清单更新，请通过设置`NetworkConfiguration.masterUpdateInterval`属性来设置更新频率（以分钟为单位）。
1. 或者，通过监听`MediaPlayerItemEvent.MASTER_UPDATED`事件来跟踪成功的清单更新。
