---
description: 可以使用MediaPlayerItemConfig类在流中配置自定义标记名称。
seo-description: 可以使用MediaPlayerItemConfig类在流中配置自定义标记名称。
seo-title: 标记的配置类方法
title: 标记的配置类方法
uuid: 222a0349-58d5-4bf3-9d03-e5920610faf5
translation-type: tm+mt
source-git-commit: b9e98ef2b4246fdfd79ebcd91db344c97367d661
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# 标记{#config-class-methods-for-tags}的配置类方法

可以使用MediaPlayerItemConfig类在流中配置自定义标记名称。

创建新`MediaPlayerItemConfig`:

```js
var mediaPlayerItemConfig = new AdobePSDK.MediPlayerItemConfig();
```

以下是关于如何使用`MediaPlayerItemConfig`方法管理自定义标记的一些信息：

<table id="table_0AC0973497144DDAB05726E3F031ACD1"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <b>订阅特定自定义标记</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&amp;nbsp;subscribeTagsObtained&amp;nbsp;=&amp;nbsp;mediaPlayerItemConfig.subscribeTags;
    </code> </td> 
   <td colname="col2"> <p>检索订阅标记的当前列表。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 
    <code class="syntax javascript">
      var&nbsp;subscribeTags&nbsp;=&nbsp;["#EXT-X-PROGRAM-DATE-TIME"];mediaPlayerItemConfig.subscribeTags&nbsp;=&nbsp;subscribeTags;
    </code> </td> 
   <td colname="col2"> <p>设置向应用程序公开的订阅标签的列表。 </p> <p>您的应用程序还会自动订阅通过<span class="codeph"> adTags </span>传输的所有标签。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <b>自定义默认机会检测器使用的广告标记  </b> </td> 
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
   <td colname="col2"> <p>设置要由默认机会生成器使用的广告标记的列表。 </p> </td> 
  </tr> 
 </tbody> 
</table>

请记住以下事项：

* 自定义标记名称必须包含`#`前缀。

   例如，`#EXT-X-ASSET`是正确的自定义标记名称，但`EXT-X-ASSET`不正确。

* 加载媒体流后，无法更改配置。

