---
description: TVSDK联系广告投放服务(例如Adobe Primetime ad decisioning)，并尝试获取与广告的视频流对应的主播放列表文件。 在广告解析阶段，TVSDK对远程广告投放服务器进行HTTP调用并解析服务器的响应。
title: 广告解析阶段
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---

# 广告解析阶段{#ad-resolving-phase}

TVSDK联系广告投放服务(例如Adobe Primetime ad decisioning)，并尝试获取与广告的视频流对应的主播放列表文件。 在广告解析阶段，TVSDK对远程广告投放服务器进行HTTP调用并解析服务器的响应。

TVSDK支持以下类型的广告提供程序：

* 元数据广告提供程序

  广告数据以纯文本JSON文件进行编码。
* Primetime ad decisioning广告提供商

  TVSDK向Primetime ad decisioning后端服务器发送请求，包括一组定位参数和资产标识号。 Primetime ad decisioning使用包含所需广告信息的SMIL（同步多媒体集成语言）文档进行响应。
* 自定义广告标记提供程序

  处理从服务器端将广告刻录到流中的情况。 TVSDK不执行实际的广告插入，但需要跟踪在服务器端插入的广告。 此提供程序设置TVSDK用于执行广告跟踪的广告标记。

在此阶段中可能会出现以下某种故障切换情况：

* 无法检索数据，原因包括缺乏连接或服务器端错误，例如无法找到资源等。
* 已检索数据，但格式无效。

  例如，出现这种情况可能是因为解析入站数据失败。

TVSDK会发出有关该错误的警告通知并继续处理。
