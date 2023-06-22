---
description: 您可以打开此功能并检查相关事件。
title: 使用实时主控清单更新
exl-id: 02cb3116-cc30-4139-841b-8d6297214b8b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 0%

---

# 使用实时主控清单更新{#use-live-master-manifest-update}

您可以打开此功能并检查相关事件。

1. 要打开实时主控清单更新，请通过设置 `NetworkConfiguration.masterUpdateInterval` 属性。
1. （可选）通过侦听 `MediaPlayerItemEvent.MASTER_UPDATED` 事件。
