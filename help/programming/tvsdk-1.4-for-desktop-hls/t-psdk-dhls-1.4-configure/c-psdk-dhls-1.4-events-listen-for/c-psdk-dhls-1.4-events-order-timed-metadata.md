---
description: 每当遇到默认或自定义标记或播放列表在清单中发生更改时，TVSDK都会调度定时元数据事件并生成定时元数据。 按事件在清单中的显示顺序调度事件。
seo-description: 每当遇到默认或自定义标记或播放列表在清单中发生更改时，TVSDK都会调度定时元数据事件并生成定时元数据。 按事件在清单中的显示顺序调度事件。
seo-title: 定时元数据事件
title: 定时元数据事件
uuid: 69c43701-6ffa-45fe-a104-fe81391222e7
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 定时元数据事件{#timed-metadata-events}

每当遇到默认或自定义标记或播放列表在清单中发生更改时，TVSDK都会调度定时元数据事件并生成定时元数据。 按事件在清单中的显示顺序调度事件。

您的播放器根据以下事件实施操作：

* `TimedMetadataEvent.TIMED_METADATA_ID3_ADDED`:在处理ID3定时元数据时调度。
* `TimedMetadataEvent.TIMED_METADATA_SKIPPED`:在处理定时元数据且未检测到业务机会时调度。

