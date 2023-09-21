---
title: 功能管理器
description: 功能管理器提供了一种方法，让您可以控制各个功能，而无需遍历整个TVSDK来搜索可能分散在多个位置的一个功能的代码。
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# 功能管理器 {#feature-managers}

功能管理器提供了一种方法，让您可以控制各个功能，而无需遍历整个TVSDK来搜索可能分散在多个位置的一个功能的代码。 功能管理器将每个功能的代码压缩为一个类。 功能管理器将等待TVSDK事件中的触发器，然后通知使用功能管理器处理结果的类。 功能管理器为类提供所需信息。

功能管理器执行以下任务：

* **触发TVSDK功能。**
这些是触发TVSDK功能的函数调用。 例如， `PlaybackManager.play()` 当播放器应用程序需要启动视频播放时，调用。

* **侦听TVSDK事件。**
功能管理器需要侦听TVSDK事件，以从TVSDK获取信息。 例如， `AdsManager` 侦听TVSDK广告事件以在广告时间开始时收到通知。

* **将事件调度到处理程序。**
功能管理器收到并处理来自TVSDK的事件后，会通知客户端处理该事件。 例如，在 `AdsManager` 接收广告时间开始事件，它告知播放器片段在UI中反映此更改（禁用推式栏、显示广告叠加等）。

Primetime参考实施包括以下功能管理器：

| 功能管理器 | 默认文件 | 功能 |  |
|---|---|---|---|
| 视频播放 | 播放管理器 | HLS播放和控制、DVR播放和控制、缓冲区控制以及多位速率处理。 | 必填 |
| DRM内容保护 | DrmManager | 内容保护。 | 必填 |
| Ad insertion | AdsManager | 广告插入，包括Adobe Primetime ad decisioning直接广告时间和自定义广告时间。 | 可选 |
| 隐藏式字幕 | CCManager | 隐藏式字幕和VTT字幕。 | 可选 |
| 后期捆绑音频 | AAManager | 延迟绑定音频。 | 可选 |
| QoS | QosManager | QoS统计数据。 | 可选 |
| 权利 | EntitlementManager | Primetime身份验证权利集成。 | 可选 |

参考实现包含上面列出的基本默认类以及后缀为On的相应类。 默认类提供默认的TVSDK行为，而带有On后缀的类包含触发TVSDK功能并监听该功能的TVSDK事件所需的所有代码。

* 对于可选功能，缺省代码的操作方式与关闭该功能相同。
* 具有On后缀的类操作方式与特征打开时相同。
