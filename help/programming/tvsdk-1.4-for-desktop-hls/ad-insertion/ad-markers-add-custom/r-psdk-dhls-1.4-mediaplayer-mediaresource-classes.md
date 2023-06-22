---
description: MediaResource表示将由MediaPlayer实例加载的内容。
title: MediaPlayer和MediaResource类
exl-id: c431c9f9-98a3-402c-b799-450f30f668dd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# MediaPlayer和MediaResource类{#mediaplayer-and-mediaresource-classes}

MediaResource表示将由MediaPlayer实例加载的内容。

<!--<a id="section_B09A012C97454AF58CE2269B800D8027"></a>-->

TVSDK库提供了一种简单的方法，用于加载和准备内容以进行播放 `replaceCurrentResource` 中的方法 `MediaPlayer` 界面。 此方法接收 `MediaResource` 类作为唯一输入参数。 此 `MediaResource` 类由以下信息组成：

* 一个URL，表示即将加载的内容的位置。
* 类型，即将加载的内容类型。

   这是一个字符串，定义可以加载的内容类型 `MediaPlayer`. 可能的值是HLS和HDS。 每个值都与表示常用文件扩展名的字符串相关联，对于HLS，为“m3u8”；对于HDS，为“f4m”。
* 某些元数据，它是 `Metadata` 类。

   此类似词典的结构可能包含有关即将加载的内容的附加信息，例如有关应放置在主内容中的替代/广告内容的信息。

元数据是将与替代内容相关的信息传递到TVSDK的媒介。 此 `Metadata` 接口定义通用键值存储的API，其中键和值都是纯字符串。
