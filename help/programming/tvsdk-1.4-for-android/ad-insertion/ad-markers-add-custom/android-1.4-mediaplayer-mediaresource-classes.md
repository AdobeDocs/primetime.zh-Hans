---
description: MediaResource表示将由MediaPlayer实例加载的内容。
title: MediaPlayer和MediaResource类
exl-id: d3ac1a8d-3549-417a-83e9-c561a3d12127
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# MediaPlayer和MediaResource类{#mediaplayer-and-mediaresource-classes}

MediaResource表示将由MediaPlayer实例加载的内容。

<!--<a id="section_B09A012C97454AF58CE2269B800D8027"></a>-->

TVSDK库提供了一种简单的方法，用于加载和准备内容以进行播放 `replaceCurrentItem` MediaPlayer界面中的方法。 此方法接收MediaResource类的实例作为唯一的输入参数。 MediaResource类由以下信息组成：

* 一个URL，表示即将加载的内容的位置。
* 类型，即将加载的内容类型。

   这是中的简单枚举 `MediaResource` 类定义可由MediaPlayer加载的内容类型。 可能的值是HLS和HDS。 每个值都与表示常用文件扩展名的字符串相关联， `m3u8` 对于HLS和 `f4m` 用于HDS。
* 某些元数据，它是 `Metadata` 类。

   此类似词典的结构可能包含有关即将加载的内容的附加信息，例如有关应放置在主内容中的替代/广告内容的信息。

元数据是将与替代内容相关的信息传递到TVSDK的媒介。 此 `Metadata` 接口定义通用键值存储的API，其中键和值都是纯字符串。
