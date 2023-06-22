---
description: 对于实时/线性内容，浏览器TVSDK会使用相同持续时间的广告时间替换主流内容的块，以便时间轴持续时间保持不变。
title: 实时/线性广告解析和插入
exl-id: 5d5954c6-9d1c-4900-9813-d3248fd61911
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 0%

---

# 实时/线性广告解析和插入{#live-linear-ad-resolving-and-insertion}

对于实时/线性内容，浏览器TVSDK会使用相同持续时间的广告时间替换主流内容的块，以便时间轴持续时间保持不变。

在播放之前和播放期间，浏览器TVSDK会解析已知广告，使用相同持续时间的广告时间替换主内容的各个部分，并在必要时重新计算虚拟时间轴。 广告时间的位置由清单定义的提示点指定。

浏览器TVSDK通过以下方式插入广告：

* **前置式广告**，位于内容的开头。

即使持续时间长于或短于提示点替换持续时间，浏览器TVSDK也会接受广告时间。 默认情况下，浏览器TVSDK支持 `#EXT-X-CUE` 提示在解决和放置广告时作为有效的广告标记。 此标记需要元数据字段 `DURATION` 以秒为单位，并且提示的唯一ID为。 例如：

```
#EXT-X-CUE:DURATION=27,ID="..."
```

您可以定义并订阅其他提示（标记）。

播放开始后，视频引擎会定期刷新清单文件。 当在清单中定义的实时流或线性流中遇到提示点时，浏览器TVSDK会解析任何新广告并插入广告。 解析和插入广告后，浏览器TVSDK会再次计算虚拟时间轴并调度 `AdobePSDK.PSDKEventType.TIMELINE_UPDATED` 事件。

>[!TIP]
>
>对于实时流，浏览器TVSDK仅支持MP4和HLS前置和中置广告。
