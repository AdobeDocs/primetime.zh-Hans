---
description: MediaResource表示将由MediaPlayer实例加载的内容。
title: MediaPlayer和MediaResource类
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# MediaPlayer和MediaResource类{#mediaplayer-and-mediaresource-classes}

MediaResource表示将由MediaPlayer实例加载的内容。

<!--<a id="section_B09A012C97454AF58CE2269B800D8027"></a>-->

TVSDK库提供了一种简单的方法，用于加载和准备内容以供播放，方法是 `replaceCurrentItem` MediaPlayer界面中的方法。 此方法接收MediaResource类的实例作为唯一输入参数。 MediaResource类由以下信息组成：

* URL，表示即将加载的内容位置。
* 类型，即将加载的内容类型。

  这是中的简单枚举 `MediaResource` 类用于定义MediaPlayer可以加载的内容类型。 可能的值是HLS和HDS。 每个值都与表示常用文件扩展名的字符串关联， `m3u8` 适用于HLS和 `f4m` 用于HDS。
* 某些元数据，这是 `Metadata` 类。

  此类似字典的结构可能包含有关即将加载的内容的附加信息，例如有关应该放置在主内容中的替代/广告内容的信息。

元数据是将与替代内容相关的信息传递到TVSDK的媒介。 此 `Metadata` 接口定义通用键值存储的API，其中键和值均为纯字符串。
