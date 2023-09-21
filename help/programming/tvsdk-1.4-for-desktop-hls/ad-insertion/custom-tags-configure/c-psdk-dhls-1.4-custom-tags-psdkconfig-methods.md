---
description: 您可以使用MediaPlayerItemConfig类在TVSDK中全局配置自定义标记名称，也可以使用MediaPlayerItemConfig类基于流配置自定义标记名称。
title: 标记的配置类方法
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# 标记的配置类方法{#config-class-methods-for-tags}

您可以使用MediaPlayerItemConfig类在TVSDK中全局配置自定义标记名称，也可以使用MediaPlayerItemConfig类基于流配置自定义标记名称。

TVSDK会自动将全局配置应用于未指定流特定配置的任何媒体流。

两者 `PSDKConfig` 和 `MediaPlayerItemConfig` 公开以下方法以管理自定义标记：

<table id="table_B37A6C75270D47BC99258F2884AD6905"> 
 <tbody> 
  <tr> 
   <td colname="1"><b>订阅特定的自定义标记</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> public函数get subscribeTags()：Vector。&lt;String&gt;</span> </td> 
   <td colname="col2"> 检索当前订阅的标记列表。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 公共函数集subscribeTags()：Vector。&lt;String&gt;</span> </td> 
   <td colname="col2">设置将向应用程序公开的订阅标记的列表。 <p>您的应用程序还会自动订阅通过传输的所有标记 <span class="codeph"> adTags</span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="1"><b>自定义默认机会检测器使用的广告标记 </b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 公共函数get adTags()：Vector。&lt;String&gt;</span> </td> 
   <td colname="col2"> 检索当前的广告标记列表。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 公共函数集adTags()：Vector。&lt;String&gt;</span> </td> 
   <td colname="col2"> 设置默认机会生成器将使用的广告标记列表。 </td> 
  </tr> 
 </tbody> 
</table>

请记住以下内容：

* setter方法不允许tags参数包含null值。

  如果遇到，TVSDK会引发 `IllegalArgumentException`.
* 自定义标记名称必须包含#前缀。

  例如， `#EXT-X-ASSET` 是正确的自定义标记名称，但 `EXT-X-ASSET` 不正确。
* 加载媒体流后，无法更改配置。
