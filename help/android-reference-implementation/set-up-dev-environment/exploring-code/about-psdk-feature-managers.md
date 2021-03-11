---
title: 功能管理器
description: 功能管理器为您提供一种控制个别功能的方式，而无需遍历整个TVSDK来搜索可能分散在多个位置的某个功能的代码。
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 1%

---


# 功能管理器{#feature-managers}

功能管理器为您提供一种控制个别功能的方式，而无需遍历整个TVSDK来搜索可能分散在多个位置的某个功能的代码。 功能管理器将代码浓缩为每个功能的一个类。 功能管理器等待TVSDK事件的触发器，然后通知使用功能管理器处理结果的类。 功能管理器为类提供所需的信息。

功能管理器执行以下任务:

* **触发TVSDK功能。**
这些是触发TVSDK功能的函数调用。例如， 
`PlaybackManager.play()` 当播放器应用程序需要开始视频播放时调用。

* **监听TVSDK事件。**
功能管理器需要监听TVSDK事件以从TVSDK获取信息。例如， 
`AdsManager` 监听TVSDK广告事件，在广告中断开始时收到通知。

* **将事件调度给处理程序。**
功能管理器从TVSDK接收并处理事件后，通知客户端处理事件。例如， 
`AdsManager` 接收广告中断开始事件，它告知播放器片段在UI中反映此更改（禁用划动栏、显示广告叠加等）。

Primetime参考实施包括以下功能管理器：

| 功能管理器 | 默认文件 | 功能 |  |
|---|---|---|---|
| 视频播放 | PlaybackManager | HLS回放和控制、DVR回放和控制、缓冲区控制和多位速率处理。 | 必需 |
| DRM内容保护 | DrmManager | 内容保护。 | 必需 |
| 广告插入 | AdsManager | 广告插入，包括Adobe Primetime广告决策直接广告中断和自定义广告中断。 | 可选 |
| 隐藏式字幕 | CCManager | 隐藏式字幕和VTT字幕。 | 可选 |
| 延迟绑定音频 | AAManager | 延迟绑定音频。 | 可选 |
| QoS | QosManager | QoS统计。 | 可选 |
| 授权 | EntitlementManager | Primetime身份验证授权集成。 | 可选 |

引用实现包含上面列出的基本默认类以及后缀为On的相应类。 默认类提供默认的TVSDK行为，而具有“打开”后缀的类包含触发TVSDK功能并侦听TVSDK事件所需的所有代码。

* 对于可选功能，默认代码的操作方式与关闭该功能一样。
* 具有“打开”后缀的类的操作就像打开特征一样。