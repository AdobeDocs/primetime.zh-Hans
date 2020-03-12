---
description: MediaResource表示MediaPlayer实例将要加载的内容。
seo-description: MediaResource表示MediaPlayer实例将要加载的内容。
seo-title: MediaPlayer和MediaResource类
title: MediaPlayer和MediaResource类
uuid: 36ef75f3-08f7-4fc5-88a7-9bab9198b917
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# MediaPlayer和MediaResource类{#mediaplayer-and-mediaresource-classes}

MediaResource表示MediaPlayer实例将要加载的内容。

<!--<a id="section_B09A012C97454AF58CE2269B800D8027"></a>-->

TVSDK库提供了一种简单的方法，可使用界面中的方法加载和准备 `replaceCurrentResource` 要回放的 `MediaPlayer` 内容。 此方法接收类的一个实 `MediaResource` 例作为唯一的输入参数。 该 `MediaResource` 类由以下信息组成：

* 一个URL，它表示要加载的内容的位置。
* 类型，即要加载的内容类型。

   这是一个字符串，它定义了可由加载的内容的类型 `MediaPlayer`。 可能的值为HLS和HDS。 每个值都与表示常用文件扩展名的字符串关联，即HLS为“m3u8”,HDS为“f4m”。
* 某些元数据，它是类的一个实 `Metadata` 例。

   此类似字典的结构可能包含有关要加载的内容的其他信息，例如关于应放置在主内容中的备用／广告内容的信息。

元数据是将与替代内容相关的信息传递到TVSDK的介质。 接 `Metadata` 口为通用键值存储定义API，其中键和值都是纯字符串。
