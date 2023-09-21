---
description: 您可以打开此功能并检查相关事件。
title: 使用实时主清单更新
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 0%

---

# 使用实时主清单更新{#use-live-master-manifest-update}

您可以打开此功能并检查相关事件。

1. 要打开实时主清单更新，请通过设置 `NetworkConfiguration.masterUpdateInterval` 属性。
1. （可选）通过侦听 `MediaPlayerItemEvent.MASTER_UPDATED` 事件。
