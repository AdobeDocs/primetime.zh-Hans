---
description: MediaResource类表示要由MediaPlayer实例加载的内容。
title: 创建媒体资源
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# 创建媒体资源 {#create-a-media-resource}

对于每个新视频内容，使用有关视频内容的信息初始化MediaResource实例并加载媒体资源。

MediaResource类表示要由MediaPlayer实例加载的内容。

1. 创建 `MediaResource` 将介质的相关信息传递给 `MediaResource` 构造函数。

   此 `MediaResource` 构造函数需要以下参数：

   <table id="table_22886D6770FB45E99D35D0B90E6CC302"> 
   <thead> 
   <tr> 
      <th colname="col1" class="entry"> 构造函数参数 </th> 
      <th colname="col2" class="entry"> 描述 </th> 
   </tr> 
   </thead>
   <tbody> 
   <tr> 
      <td colname="col1"> <span class="codeph"> url </span> </td> 
      <td colname="col2"> 表示媒体的清单/播放列表的URL的字符串。 </td> 
   </tr> 
   <tr> 
      <td colname="col1"> <span class="codeph"> type </span> </td> 
      <td colname="col2"> 下列成员之一 <span class="codeph"> MediaResource.Type </span> 枚举，对应于指示的文件类型： 
      <ul id="ul_C286ED3C31364B858A1C9AF3356E9282"> 
      <li id="li_25B24EF76D8849DE8764539F25E435FA"> <span class="codeph"> HLS </span> - M3U8 </li> 
      <li id="li_1344A41B434D49229E392F1AAF9ECA81"> <span class="codeph"> ISOBMFF </span> - ISO基本媒体文件格式(MP4) </li> 
      <li id="li_92392073B7334916B06B16570C51AC91"> <span class="codeph"> 短划线 </span> - MPEG-DASH媒体演示文稿描述(MPD) </li> 
      </ul> </td> 
   </tr> 
   <tr> 
      <td colname="col1"> <span class="codeph"> 元数据 </span> </td> 
      <td colname="col2"> 的实例 <span class="codeph"> 元数据 </span> 类（类似字典的结构），可能包含有关即将加载的内容的其他信息，例如要放置在主内容中的替换内容或广告内容。 如果使用广告，请设置 <span class="codeph"> Auditudesettings </span> 使用此构造函数之前 <a href="/help/programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-insertion-metadata/android-3x-ad-insertion-metadata.md"> 广告插入元数据 </a>. </td> 
   </tr> 
   </tbody> 
   </table>

   >[!IMPORTANT]
   >
   >TVSDK仅支持特定内容类型的播放。 如果您尝试加载任何其他类型的内容，TVSDK会调度错误事件。
   >
   >对于MP4视频点播(VOD)内容，TVSDK不支持特技播放、自适应比特率(ABR)流、广告插入、隐藏式字幕或DRM。

   以下代码创建 `MediaResource` 实例： >

   ```java
   // To do: Create metadata here 
   MediaResource res = new MediaResource( 
     "https://www.example.com/video/some-video.m3u8",  
   MediaResource.Type.HLS, 
     metadata); 
   ```

   在此步骤后的任何时间，您都可以使用 `MediaResource` 访问器(getter) ，用于检查资源的类型、URL和元数据。

1. 使用以下选项之一加载媒体资源：

   * MediaPlayer实例。
   * `MediaPlayerItemLoader` 有关更多信息，请参阅 [使用MediaPlayerItemLoader加载媒体资源](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

   >[!IMPORTANT]
   >
   >请勿在后台线程上加载媒体资源。 大多数TVSDK操作需要在主线程上运行，而在后台线程上运行这些操作可能会导致操作抛出错误并退出。
