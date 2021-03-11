---
description: TVSDK在遇到默认或自定义标记或播放列表在清单中发生更改时调度定时元数据事件并生成定时元数据。 事件按在清单中显示的顺序进行调度。
title: 定时元数据事件
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---


# 定时元数据事件{#timed-metadata-events}

TVSDK在遇到默认或自定义标记或播放列表在清单中发生更改时调度定时元数据事件并生成定时元数据。 事件按在清单中显示的顺序进行调度。

您的播放器根据以下事件实现操作：

* `TimedMetadataEvent.TIMED_METADATA_ID3_ADDED`:在处理ID3定时元数据时调度。
* `TimedMetadataEvent.TIMED_METADATA_SKIPPED`:在处理定时元数据且未检测到任何机会时调度。

