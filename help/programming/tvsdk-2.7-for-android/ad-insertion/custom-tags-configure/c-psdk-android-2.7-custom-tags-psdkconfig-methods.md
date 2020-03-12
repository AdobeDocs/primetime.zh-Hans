---
description: 您可以使用MediaPlayerItemConfig类在TVSDK中全局配置自定义标记名称。
seo-description: 您可以使用MediaPlayerItemConfig类在TVSDK中全局配置自定义标记名称。
seo-title: 标记的配置类方法
title: 标记的配置类方法
uuid: 64284876-1f31-47e0-a99b-3bfe17e10707
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 标记的配置类方法 {#config-class-methods-for-tags}

您可以使用MediaPlayerItemConfig类在TVSDK中全局配置自定义标记名称。

TVSDK会自动将全局配置应用于任何未指定流特定配置的媒体流。

`MediaPlayerItemConfig` 显示这些方法以管理自定义标记：

<table id="table_B37A6C75270D47BC99258F2884AD6905"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <b>订阅特定的自定义标记</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final String[] getSubscriptedTags </span> </td> 
   <td colname="col2"> <p>检索订阅标记的当前列表。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final void setSubscribedTags（String[]标签）; </span> </td> 
   <td colname="col2"> <p>设置将向应用程序公开的订阅标记列表。 </p> <p>您的应用程序还会自动订阅通过setAdTags传输的所 <span class="codeph"> 有标签 </span>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <b>自定义默认业务机会检测器使用的广告标记</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final String[] getAdTags; </span> </td> 
   <td colname="col2"> <p>检索广告标记的当前列表。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final void setAdTags(String[] tags); </span> </td> 
   <td colname="col2"> <p>设置默认业务机会生成器将使用的广告标记列表。 </p> </td> 
  </tr> 
 </tbody> 
</table>

请记住以下事项：

* setter方法不允许标记参数包含null值。

   如果遇到，TVSDK将引发 `IllegalArgumentException`。
* 自定义标记名称必须包含前 `#` 缀。

   例如，自定 `#EXT-X-ASSET` 义标记名称正确，但 `EXT-X-ASSET` 不正确。

* 加载媒体流后，无法更改配置。
