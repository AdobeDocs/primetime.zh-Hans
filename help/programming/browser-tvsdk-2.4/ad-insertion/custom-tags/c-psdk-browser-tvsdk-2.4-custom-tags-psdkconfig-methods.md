---
description: 您可以使用MediaPlayerItemConfig类在流中配置自定义标记名称。
title: 标记的配置类方法
exl-id: 864d5c35-2b26-447b-8134-414e82096f18
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# 标记的配置类方法{#config-class-methods-for-tags}

您可以使用MediaPlayerItemConfig类在流中配置自定义标记名称。

新建 `MediaPlayerItemConfig`：

```js
var mediaPlayerItemConfig = new AdobePSDK.MediPlayerItemConfig();
```

以下是关于如何 `MediaPlayerItemConfig` 方法用于管理自定义标记：

<table id="table_0AC0973497144DDAB05726E3F031ACD1"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <b>订阅特定的自定义标记</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&amp;nbsp;subscribeTagsObtained&amp;nbsp;=&amp;nbsp;mediaPlayerItemConfig.subscribeTags;
    </code> </td> 
   <td colname="col2"> <p>检索订阅标签的当前列表。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&nbsp;subscribeTags&nbsp;=&nbsp;["#EXT-X-PROGRAM-DATE-TIME"];mediaPlayerItemConfig.subscribeTags&nbsp;=&nbsp;subscribeTags;
    </code> </td> 
   <td colname="col2"> <p>设置向应用程序公开的订阅标记的列表。 </p> <p>您的应用程序还会自动订阅通过传输的所有标记 <span class="codeph"> adtags </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <b>自定义默认机会检测器使用的广告标记 </b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&amp;nbsp;adTagsObtained&amp;nbsp;=&amp;nbsp;mediaPlayerItemConfig.adTags; 
    </code> </td> 
   <td colname="col2"> <p>检索广告标记的当前列表。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&nbsp;adTags&nbsp;=&nbsp;["#EXT-X-CUE"];mediaPlayerItemConfig.adTags&nbsp;=&nbsp;adTags;
    </code> </td> 
   <td colname="col2"> <p>设置默认机会生成器使用的广告标记列表。 </p> </td> 
  </tr> 
 </tbody> 
</table>

请记住以下内容：

* 自定义标记名称必须包含 `#` 前缀。

   例如， `#EXT-X-ASSET` 是正确的自定义标记名称，但是 `EXT-X-ASSET` 不正确。

* 加载媒体流后，无法更改配置。
