---
description: 您可以打开此功能并检查相关事件。
title: 使用实时主控清单更新
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 0%

---


# 使用实时主控清单更新{#use-live-master-manifest-update}

您可以打开此功能并检查相关事件。

1. 要打开实时主控清单更新，请通过设置`NetworkConfiguration.masterUpdateInterval`属性来设置更新频率（以分钟为单位）。
1. 或者，通过侦听`MediaPlayerItemEvent.MASTER_UPDATED`事件来跟踪成功的清单更新。
