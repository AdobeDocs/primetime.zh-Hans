---
description: 可以在TVSDK中使用MediaPlayerItemConfig类全局配置自定义标记名称，或使用MediaPlayerItemConfig类基于流。
seo-description: 可以在TVSDK中使用MediaPlayerItemConfig类全局配置自定义标记名称，或使用MediaPlayerItemConfig类基于流。
seo-title: 标记的配置类方法
title: 标记的配置类方法
uuid: 3317fc8b-c13c-4e7d-8334-aa8cdf40fa05
translation-type: tm+mt
source-git-commit: b9e98ef2b4246fdfd79ebcd91db344c97367d661

---


# 标记的配置类方法{#config-class-methods-for-tags}

可以在TVSDK中使用MediaPlayerItemConfig类全局配置自定义标记名称，或使用MediaPlayerItemConfig类基于流。

TVSDK会自动将全局配置应用于任何未指定流特定配置的媒体流。

同时 `PSDKConfig` 显示 `MediaPlayerItemConfig` 和显示这些方法以管理自定义标记：

<table id="table_B37A6C75270D47BC99258F2884AD6905"> 
 <tbody> 
  <tr> 
   <td colname="1"><b>订阅特定的自定义标记</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> public函数get subscribeTags():Vector.&lt;String&gt;</span> </td> 
   <td colname="col2"> 检索订阅标记的当前列表。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> public函数集subscribeTags():Vector.&lt;String&gt;</span> </td> 
   <td colname="col2">设置将向应用程序公开的订阅标记列表。 <p>您的应用程序还会自动订阅通过adTags传输的所 <span class="codeph"> 有标签</span>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="1"><b>自定义默认业务机会检测器使用的广告标记 </b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> public函数get adTags():Vector.&lt;String&gt;</span> </td> 
   <td colname="col2"> 检索广告标记的当前列表。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> public function set adTags():Vector.&lt;String&gt;</span> </td> 
   <td colname="col2"> 设置默认业务机会生成器将使用的广告标记列表。 </td> 
  </tr> 
 </tbody> 
</table>

请记住以下事项：

* setter方法不允许标记参数包含null值。

   如果遇到，TVSDK将引发 `IllegalArgumentException`。
* 自定义标记名称必须包含#前缀。

   例如，自定 `#EXT-X-ASSET` 义标记名称正确，但 `EXT-X-ASSET` 不正确。
* 加载媒体流后，无法更改配置。

