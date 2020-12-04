---
description: MediaResource表示MediaPlayer实例将要加载的内容。
seo-description: MediaResource表示MediaPlayer实例将要加载的内容。
seo-title: MediaPlayer和MediaResource类
title: MediaPlayer和MediaResource类
uuid: 7393c320-7dbb-4580-9425-a735f9d03ef5
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---


# MediaPlayer和MediaResource类{#mediaplayer-and-mediaresource-classes}

MediaResource表示MediaPlayer实例将要加载的内容。

<!--<a id="section_B09A012C97454AF58CE2269B800D8027"></a>-->

TVSDK库提供了一种简单的方法，通过在MediaPlayer界面中使用`replaceCurrentItem`方法加载和准备要回放的内容。 此方法接收MediaResource类的一个实例作为唯一输入参数。 MediaResource类由以下信息组成：

* 一个URL，它表示要加载的内容的位置。
* 一种类型，即要加载的内容的类型。

   这是`MediaResource`类中的一个简单明细列表，它定义MediaPlayer可以加载的内容类型。 可能的值是HLS和HDS。 每个值都与表示常用文件扩展名的字符串相关联，HLS的`m3u8`和HDS的`f4m`。
* 某些元数据，它是`Metadata`类的实例。

   此类似字典的结构可能包含有关要加载的内容的其他信息，例如关于应放在主内容中的备用／广告内容的信息。

元数据是将与替代内容相关的信息传递到TVSDK的媒介。 `Metadata`接口为通用key-value存储定义API，其中键和值都是纯字符串。
