---
description: MediaResource表示MediaPlayer实例将要加载的内容。
seo-description: MediaResource表示MediaPlayer实例将要加载的内容。
seo-title: MediaPlayer和MediaResource类
title: MediaPlayer和MediaResource类
uuid: 7393c320-7dbb-4580-9425-a735f9d03ef5
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# MediaPlayer和MediaResource类{#mediaplayer-and-mediaresource-classes}

MediaResource表示MediaPlayer实例将要加载的内容。

<!--<a id="section_B09A012C97454AF58CE2269B800D8027"></a>-->

TVSDK库提供了一种简单的方法，可使用MediaPlayer界面中的方法加载和准备 `replaceCurrentItem` 要回放的内容。 此方法接收MediaResource类的一个实例作为唯一输入参数。 MediaResource类由以下信息组成：

* 一个URL，它表示要加载的内容的位置。
* 类型，即要加载的内容类型。

   这是类中的一个简单枚举， `MediaResource` 它定义了MediaPlayer可以加载的内容类型。 可能的值为HLS和HDS。 每个值都与表示HLS和HDS常用文件扩展名 `m3u8` 的字符串 `f4m` 相关联。
* 某些元数据，它是类的一个实 `Metadata` 例。

   此类似字典的结构可能包含有关要加载的内容的其他信息，例如关于应放置在主内容中的备用／广告内容的信息。

元数据是将与替代内容相关的信息传递到TVSDK的介质。 接 `Metadata` 口为通用键值存储定义API，其中键和值都是纯字符串。
