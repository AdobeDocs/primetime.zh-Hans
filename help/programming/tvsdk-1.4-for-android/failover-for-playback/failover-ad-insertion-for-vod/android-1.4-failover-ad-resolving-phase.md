---
description: TVSDK与广告投放服务(如Adobe Primetime广告决策)联系，并尝试获取与广告的视频流对应的主播放列表文件。 在广告解析阶段，TVSDK对远程广告投放服务器进行HTTP调用并解析服务器的响应。
title: 广告分析阶段
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---


# 广告分辨阶段{#ad-resolving-phase}

TVSDK与广告投放服务(如Adobe Primetime广告决策)联系，并尝试获取与广告的视频流对应的主播放列表文件。 在广告解析阶段，TVSDK对远程广告投放服务器进行HTTP调用并解析服务器的响应。

TVSDK支持以下类型的广告提供者：

* 元数据广告提供商

   广告数据以纯文本JSON文件进行编码。
* Primetime广告决策广告提供商

   TVSDK向Primetime广告决策后端服务器发送请求，包括一组定位参数和资产标识号。 Primetime广告决策采用包含所需广告信息的SMIL（同步多媒体集成语言）文档做出响应。
* 自定义广告标记提供者

   处理从服务器端将广告刻录到流中的情况。 TVSDK不执行实际广告插入，但需要跟踪在服务器端插入的广告。 此提供者设置TVSDK用于执行广告跟踪的广告标记。

在此阶段中，可能发生以下故障切换情形之一：

* 无法检索数据，原因包括缺少连接或服务器端错误，如找不到资源等。
* 已检索数据，但格式无效。

   这可能是因为，例如，分析入站数据失败。

TVSDK发出有关该错误的警告通知并继续处理。
