---
description: TVSDK调度定时元数据事件，并在遇到默认或自定义标记或清单中的播放列表更改时生成定时元数据。 事件按其在清单中的显示顺序进行调度。
seo-description: TVSDK调度定时元数据事件，并在遇到默认或自定义标记或清单中的播放列表更改时生成定时元数据。 事件按其在清单中的显示顺序进行调度。
seo-title: 定时元数据事件
title: 定时元数据事件
uuid: 69c43701-6ffa-45fe-a104-fe81391222e7
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---


# 定时元数据事件{#timed-metadata-events}

TVSDK调度定时元数据事件，并在遇到默认或自定义标记或清单中的播放列表更改时生成定时元数据。 事件按其在清单中的显示顺序进行调度。

您的播放器根据以下事件实现操作：

* `TimedMetadataEvent.TIMED_METADATA_ID3_ADDED`:在处理ID3定时元数据时调度。
* `TimedMetadataEvent.TIMED_METADATA_SKIPPED`:在处理定时元数据且未检测到任何机会时调度。

