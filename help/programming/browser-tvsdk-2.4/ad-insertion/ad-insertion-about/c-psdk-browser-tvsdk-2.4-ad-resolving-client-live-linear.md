---
description: 对于实时/线性内容，Browser TVSDK将主流内容的块替换为相同持续时间的广告中断，以便时间线持续时间保持不变。
title: 实时/线性广告解析和插入
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 0%

---


# 实时/线性广告解析和插入{#live-linear-ad-resolving-and-insertion}

对于实时/线性内容，Browser TVSDK将主流内容的块替换为相同持续时间的广告中断，以便时间线持续时间保持不变。

在播放之前和播放过程中，Browser TVSDK会解析已知广告，用相同持续时间的广告中断替换部分主内容，并在必要时重新计算虚拟时间轴。 广告断点的位置由清单定义的提示点指定。

浏览器TVSDK以下列方式插入广告：

* **前置**，内容的开头。

即使持续时间长于或短于提示点替换持续时间，浏览器TVSDK也接受广告中断。 默认情况下，Browser TVSDK在解析和放置广告时支持将`#EXT-X-CUE`提示作为有效的广告标记。 此标记要求元数据字段`DURATION`（以秒为单位）和提示的唯一ID。 例如：

```
#EXT-X-CUE:DURATION=27,ID="..."
```

您可以定义和订阅其他提示（标记）。

播放开始后，视频引擎会定期刷新清单文件。 浏览器TVSDK解析任何新广告，并在清单中定义的实时或线性流中遇到提示点时插入广告。 解析并插入广告后，Browser TVSDK将再次计算虚拟时间轴并调度`AdobePSDK.PSDKEventType.TIMELINE_UPDATED`事件。

>[!TIP]
>
>对于直播流，浏览器TVSDK仅支持MP4和HLS前摄和中摄广告。

