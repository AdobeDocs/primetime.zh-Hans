---
description: 您可以使用MediaPlayerItemConfig类在TVSDK中全局配置自定义标记名称。
title: 标记的配置类方法
exl-id: 48e88284-788c-49b3-a370-3e3d77a8da6f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# 标记的配置类方法 {#config-class-methods-for-tags}

您可以使用MediaPlayerItemConfig类在TVSDK中全局配置自定义标记名称。

TVSDK会自动将全局配置应用于未指定流特定配置的任何媒体流。

`MediaPlayerItemConfig` 显示以下方法以管理自定义标记：

<table id="table_B37A6C75270D47BC99258F2884AD6905"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <b>订阅特定的自定义标记</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final String[] getSubscribedTags </span> </td> 
   <td colname="col2"> <p>检索订阅标签的当前列表。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 公共最终void setSubscribedTags（String[]标记）； </span> </td> 
   <td colname="col2"> <p>设置将向应用程序公开的订阅标记的列表。 </p> <p>您的应用程序也将自动订阅通过传输的所有标记 <span class="codeph"> setadtags </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <b>自定义默认机会检测器使用的广告标记</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public final String[] getAdTags； </span> </td> 
   <td colname="col2"> <p>检索广告标记的当前列表。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 公共最终void setAdTags（String[]标记）； </span> </td> 
   <td colname="col2"> <p>设置默认机会生成器将使用的广告标记列表。 </p> </td> 
  </tr> 
 </tbody> 
</table>

请记住以下内容：

* setter方法不允许tags参数包含null值。

   如果遇到这种情况，TVSDK会引发 `IllegalArgumentException`.
* 自定义标记名称必须包含 `#` 前缀。

   例如， `#EXT-X-ASSET` 是正确的自定义标记名称，但是 `EXT-X-ASSET` 不正确。

* 加载媒体流后，无法更改配置。
