---
description: 每当遇到默认或自定义标记或在清单中播放列表发生更改时，TVSDK会调度定时元数据事件并生成定时元数据。 事件按照它们在清单中的显示顺序进行调度。
title: 定时元数据事件
exl-id: 4c58b06e-5f70-452c-a743-55c4b6206711
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# 定时元数据事件{#timed-metadata-events}

每当遇到默认或自定义标记或在清单中播放列表发生更改时，TVSDK会调度定时元数据事件并生成定时元数据。 事件按照它们在清单中的显示顺序进行调度。

您的播放器根据以下事件实施操作：

* `TimedMetadataEvent.TIMED_METADATA_ID3_ADDED`：在处理ID3定时元数据时调度。
* `TimedMetadataEvent.TIMED_METADATA_SKIPPED`：在处理定时元数据时调度，并且未检测到机会。
