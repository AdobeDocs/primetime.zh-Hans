---
description: MediaResource表示MediaPlayer实例将要加载的内容。
title: MediaPlayer和MediaResource类
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---


# MediaPlayer和MediaResource类{#mediaplayer-and-mediaresource-classes}

MediaResource表示MediaPlayer实例将要加载的内容。

<!--<a id="section_B09A012C97454AF58CE2269B800D8027"></a>-->

TVSDK库提供了一种简单的方法，可使用`MediaPlayer`接口中的`replaceCurrentResource`方法加载和准备要回放的内容。 此方法接收作为唯一输入参数的`MediaResource`类的实例。 `MediaResource`类由以下信息组成：

* 一个URL，它表示要加载的内容的位置。
* 一种类型，即要加载的内容的类型。

   这是一个字符串，它定义了`MediaPlayer`可加载的内容类型。 可能的值是HLS和HDS。 每个值都与表示常用文件扩展名的字符串关联，即HLS的“m3u8”和HDS的“f4m”。
* 某些元数据，它是`Metadata`类的实例。

   此类似词典的结构可能包含有关要加载的内容的其他信息，例如关于应放置在主内容中的备用/广告内容的信息。

元数据是与替代内容相关的信息传递到TVSDK的媒介。 `Metadata`接口为通用key-value存储定义API，其中键和值都是纯字符串。
