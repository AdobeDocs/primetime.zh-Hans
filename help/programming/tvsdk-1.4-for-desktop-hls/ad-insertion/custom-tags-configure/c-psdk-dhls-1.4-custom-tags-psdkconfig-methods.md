---
description: 您可以在TVSDK中使用MediaPlayerItemConfig类全局配置自定义标记名称，或使用MediaPlayerItemConfig类基于流配置自定义标记名称。
seo-description: 您可以在TVSDK中使用MediaPlayerItemConfig类全局配置自定义标记名称，或使用MediaPlayerItemConfig类基于流配置自定义标记名称。
seo-title: 标记的配置类方法
title: 标记的配置类方法
uuid: 3317fc8b-c13c-4e7d-8334-aa8cdf40fa05
translation-type: tm+mt
source-git-commit: b9e98ef2b4246fdfd79ebcd91db344c97367d661
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# 标记{#config-class-methods-for-tags}的配置类方法

您可以在TVSDK中使用MediaPlayerItemConfig类全局配置自定义标记名称，或使用MediaPlayerItemConfig类基于流配置自定义标记名称。

TVSDK会自动将全局配置应用于任何未指定流特定配置的媒体流。

`PSDKConfig`和`MediaPlayerItemConfig`都提供以下方法来管理自定义标记：

<table id="table_B37A6C75270D47BC99258F2884AD6905"> 
 <tbody> 
  <tr> 
   <td colname="1"><b>订阅特定自定义标记</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 公共函数get subscribeTags():Vector。&lt;string&gt;</span> </td> 
   <td colname="col2"> 检索订阅标记的当前列表。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 公共函数集subscribeTags():Vector。&lt;string&gt;</span> </td> 
   <td colname="col2">设置将向应用程序公开的订阅标记的列表。 <p>您的应用程序还会自动订阅通过<span class="codeph"> adTags</span>传输的所有标签。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="1"><b>自定义默认机会检测器使用的广告标记  </b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 公共函数get adTags():Vector。&lt;string&gt;</span> </td> 
   <td colname="col2"> 检索广告标记的当前列表。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 公共函数集adTags():Vector。&lt;string&gt;</span> </td> 
   <td colname="col2"> 设置默认业务机会生成器将使用的广告标记的列表。 </td> 
  </tr> 
 </tbody> 
</table>

请记住以下事项：

* setter方法不允许标记参数包含null值。

   如果遇到，TVSDK将引发`IllegalArgumentException`。
* 自定义标记名称必须包含#前缀。

   例如，`#EXT-X-ASSET`是正确的自定义标记名称，但`EXT-X-ASSET`不正确。
* 加载媒体流后，无法更改配置。

