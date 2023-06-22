---
title: 功能管理器
description: 功能管理器提供了一种方法，让您可以控制各个功能，而无需遍历整个TVSDK来搜索可能分散在多个位置的一个功能的代码。
exl-id: dbf2dc8b-6067-4d94-9c3c-553452b7ffd9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# 功能管理器 {#feature-managers}

功能管理器提供了一种方法，让您可以控制各个功能，而无需遍历整个TVSDK来搜索可能分散在多个位置的一个功能的代码。 功能管理器将代码压缩为每个功能的一个类。 功能管理器等待TVSDK事件中的触发器，然后通知使用功能管理器处理结果的类。 功能管理器为类提供所需信息。

功能管理器执行以下任务：

* **触发TVSDK功能。**
这些是触发TVSDK功能的函数调用。 例如， 
`PlaybackManager.play()` 当播放器应用程序需要启动视频播放时，调用。

* **侦听TVSDK事件。**
功能管理器需要侦听TVSDK事件，以从TVSDK获取信息。 例如， 
`AdsManager` 收听TVSDK广告事件以在广告时间开始时获得通知。

* **将事件调度到处理程序。**
功能管理器从TVSDK接收并处理事件后，会通知客户端处理该事件。 例如，在 
`AdsManager` 接收广告时间开始事件，通知播放器片段在UI中反映此更改（禁用推式栏、显示广告叠加等）。

Primetime参考实施包括以下功能管理器：

| 功能管理器 | 默认文件 | 功能 |  |
|---|---|---|---|
| 视频播放 | 播放管理器 | HLS播放和控制、DVR播放和控制、缓冲器控制以及多位速率处理。 | 必需 |
| DRM内容保护 | DrmManager | 内容保护。 | 必需 |
| 广告插入 | 广告管理器 | 广告插入，包括Adobe Primetime ad decisioning直接广告时间以及自定义广告时间。 | 可选 |
| 隐藏字幕 | CCManager | 隐藏式字幕和VTT字幕。 | 可选 |
| 后期绑定音频 | AAManager | 延迟绑定音频。 | 可选 |
| 服务质量 | QosManager | QoS统计数据。 | 可选 |
| 权利 | EntitlementManager | Primetime身份验证权利集成。 | 可选 |

引用实现包含上面列出的基本默认类以及后缀为On的相应类。 默认类提供默认的TVSDK行为，而具有On后缀的类包含触发TVSDK功能并监听该功能的TVSDK事件所需的所有代码。

* 对于可选功能，默认代码的运行方式与功能关闭时相同。
* 具有On后缀的类操作方式与特征打开时相同。
