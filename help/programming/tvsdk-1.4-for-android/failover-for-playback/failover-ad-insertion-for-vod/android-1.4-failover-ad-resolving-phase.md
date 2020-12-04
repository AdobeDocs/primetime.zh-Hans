---
description: TVSDK与广告投放服务(如Adobe Primetime广告决策)联系，并尝试获取与广告视频流对应的主播放列表文件。 在广告解析阶段，TVSDK对远程广告投放服务器进行HTTP调用并解析服务器的响应。
seo-description: TVSDK与广告投放服务(如Adobe Primetime广告决策)联系，并尝试获取与广告视频流对应的主播放列表文件。 在广告解析阶段，TVSDK对远程广告投放服务器进行HTTP调用并解析服务器的响应。
seo-title: 广告分析阶段
title: 广告分析阶段
uuid: b3e62a57-7e62-4e4e-8fa6-0d416785db67
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---


# 广告分辨阶段{#ad-resolving-phase}

TVSDK与广告投放服务(如Adobe Primetime广告决策)联系，并尝试获取与广告视频流对应的主播放列表文件。 在广告解析阶段，TVSDK对远程广告投放服务器进行HTTP调用并解析服务器的响应。

TVSDK支持以下类型的广告提供商：

* 元数据广告提供商

   广告数据以纯文本JSON文件进行编码。
* Primetime广告决策广告提供商

   TVSDK向Primetime广告决策后端服务器发送请求，包括一组定位参数和资产标识号。 Primetime广告决策采用包含所需广告信息的SMIL（同步多媒体集成语言）文档做出响应。
* 自定义广告标记提供者

   处理从服务器端将广告烧录到流中的情况。 TVSDK不执行实际的广告插入，但需要跟踪在服务器端插入的广告。 此提供者设置TVSDK用于执行广告跟踪的广告标记。

在此阶段可能发生以下故障转移情况之一：

* 由于连接不足或服务器端错误（如找不到资源等）等原因，无法检索数据。
* 已检索数据，但格式无效。

   这可能是因为，例如，分析入站数据失败。

TVSDK发出有关该错误的警告通知并继续处理。
