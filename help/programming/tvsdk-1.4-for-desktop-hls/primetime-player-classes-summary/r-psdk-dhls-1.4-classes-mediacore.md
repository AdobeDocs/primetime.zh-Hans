---
description: 您可以使用Primetime Player API自定义播放器的行为。 这些类描述您的媒体播放器及其资源。
title: Mediacore类
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '667'
ht-degree: 0%

---


# Mediacore类{#mediacore-classes}

您可以使用Primetime Player API自定义播放器的行为。 这些类描述您的媒体播放器及其资源。

要查看TVSDK的完整API文档，请转至[Adobe Primetime API引用](https://help.adobe.com/en_US/primetime/api/index.html)。

这些类描述您的媒体播放器及其资源。
包：[com.adobe.mediacore](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/package-detail.html)

<table frame="all" colsep="1" rowsep="1" id="table_2801E01282A948E6917910CA2FD1E05C"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> <p>名称 </p> </th> 
   <th colname="2" class="entry"> <p>说明 </p> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/ABRControlParameters.html" format="html" scope="external"> ABRControlParameters</a> </span> </td> 
   <td colname="2"> 封装所有自适应比特率控制参数的类。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/BufferControlParameters.html" format="html" scope="external"> BufferControlParameters</a></span> </td> 
   <td colname="2"> 封装所有缓冲区控制参数的类。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/ClosedCaptionStyles.html" format="html" scope="external"> ClosedCaptionsStyles</a></span> </td> 
   <td colname="2"> 定义隐藏字幕中文本的所有样式属性的类。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/ClosedCaptionsVisibility.html" format="html" scope="external"> ClosedCaptionsVisibility</a></span> </td> 
   <td colname="2"> 控制隐藏字幕是否可见的类。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/ContentFactory.html" format="html" scope="external"> ContentFactory</a> </span> </td> 
   <td colname="2"> 用于创建和管理广告工作流中使用的各种组件的工厂基类。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/DefaultAdPolicySelector.html" format="html" scope="external"> DefaultAdPolicySelector</a></span> </td> 
   <td colname="2"> 广告播放行为的默认实现。 允许应用程序自定义广告行为的界面。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/DefaultContentFactory.html" format="html" scope="external"> DefaultContentFactory</a></span> </td> 
   <td colname="2">默认实现<span class="codeph"> MediaPlayerClient</span>工厂，同时支持元数据和广告解析过程。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/DefaultMediaPlayer.html" format="html" scope="external"> DefaultMediaPlayer</a></span> </td> 
   <td colname="2"><span class="codeph"> MediaPlayer</span>接口的默认类实现。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/DefaultMediaPlayerConfig.html" format="html" scope="external"> DefaultMediaPlayerConfig</a> </span> </td> 
   <td colname="2"> 默认实现媒体播放器的配置类。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/DefaultMediaPlayerItemConfig.html" format="html" scope="external"> DefaultMediaPlayerItemConfig</a></span> </td> 
   <td colname="2"> 默认媒体播放器项配置类。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/DefaultMediaPlayerItemLoader.html" format="html" scope="external"> DefaultMediaPlayerItemLoader</a></span> </td> 
   <td colname="2"> 默认媒体播放器项加载器。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayer.html" format="html" scope="external"> MediaPlayer</a></span> </td> 
   <td colname="2"><span class="codeph"> DefaultMediaPlayer</span>类的公共接口。 包括事件、PlayerState和可见性的明细列表。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerConfig.html" format="html" scope="external"> MediaPlayerConfig</a> </span> </td> 
   <td colname="2"> 媒体播放器配置类。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerContext.html" format="html" scope="external"> MediaPlayerContext</a></span> </td> 
   <td colname="2"> 为媒体播放器提供其他上下文的类。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItem.html" format="html" scope="external"> MediaPlayerItem</a></span> </td> 
   <td colname="2"> 表示音频 — 视频媒体的界面。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/DefaultMediaPlayerItemConfig.html" format="html" scope="external"> DefaultMediaPlayerItemConfig</a></span> </td> 
   <td colname="2"> 默认媒体播放器项配置类。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html" format="html" scope="external"> MediaPlayerItemLoader</a></span> </td> 
   <td colname="2">加载媒体播放器资源并创建相应<span class="codeph"> MediaPlayerItem</span>对象的类。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerStatus.html" format="html" scope="external"> MediaPlayerStatus</a></span> </td> 
   <td colname="2"> 包含媒体播放器支持的状态的类。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerView.html" format="html" scope="external"> MediaPlayerView</a></span> </td> 
   <td colname="2">将由<span class="codeph"> MediaPlayer</span>用于视频渲染的视图的类。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaResource.html" format="html" scope="external"> 媒体资源</a></span> </td> 
   <td colname="2"> 包含有关媒体资源的所有信息的类。 包括媒体资源类型的明细列表。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaResourceType.html" format="html" scope="external"> 媒体资源类型</a></span> </td> 
   <td colname="2"> 包含受支持媒体资源类型的类。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/PSDKConfig.html" format="html" scope="external"> PSDKConfig</a></span> </td> 
   <td colname="2"> 封装媒体播放器在执行广告放置时使用的自定义标记的类，以及默认提示标记。 它还包括应用程序希望获得通知的标记名称。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/TextFormat.html" format="html" scope="external"> TextFormat</a></span> </td> 
   <td colname="2"> 封装描述文本样式（例如隐藏字幕样式）的不同属性的接口。 </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/Version.html" format="html" scope="external"> 版本</a></span> </td> 
   <td colname="2"> 提供TVSDK版本和说明的类。 </td> 
  </tr> 
 </tbody> 
</table>

