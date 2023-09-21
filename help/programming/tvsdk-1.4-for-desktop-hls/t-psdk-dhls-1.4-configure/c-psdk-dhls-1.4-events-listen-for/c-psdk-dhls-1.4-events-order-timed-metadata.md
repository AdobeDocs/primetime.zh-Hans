---
description: TVSDK会在遇到默认或自定义标记或清单中的播放列表发生更改时，调度定时元数据事件并生成定时元数据。 事件按照它们在清单中的显示顺序进行调度。
title: 定时元数据事件
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# 定时元数据事件{#timed-metadata-events}

TVSDK会在遇到默认或自定义标记或清单中的播放列表发生更改时，调度定时元数据事件并生成定时元数据。 事件按照它们在清单中的显示顺序进行调度。

您的播放器根据以下事件实施操作：

* `TimedMetadataEvent.TIMED_METADATA_ID3_ADDED`：在处理ID3定时元数据时调度。
* `TimedMetadataEvent.TIMED_METADATA_SKIPPED`：在处理定时元数据时调度，未检测到任何机会。
