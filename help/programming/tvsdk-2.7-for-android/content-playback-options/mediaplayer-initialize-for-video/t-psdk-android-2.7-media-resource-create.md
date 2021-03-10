---
description: MediaResource类表示要由MediaPlayer实例加载的内容。
title: 创建媒体资源
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---


# 创建媒体资源{#create-a-media-resource}

对于每个新的视频内容，使用有关视频内容的信息初始化一个MediaResource实例并加载媒体资源。

MediaResource类表示要由MediaPlayer实例加载的内容。

1. 通过将有关媒体的信息传递给`MediaResource`构造函数创建`MediaResource`。

   `MediaResource`构造函数需要以下参数：

   <table id="table_22886D6770FB45E99D35D0B90E6CC302">
      <thead>
      <tr>
      <th colname="col1" class="entry"> 构造函数参数 </th>
      <th colname="col2" class="entry"> 说明 </th>
      </tr>
      </thead>
      <tbody>
      <tr>
      <td colname="col1"> <span class="codeph"> url  </span> </td>
      <td colname="col2"> 一个字符串，表示媒体的清单/播放列表的URL。 </td>
      </tr>
      <tr>
      <td colname="col1"> <span class="codeph"> 类型  </span> </td>
      <td colname="col2"> <span class="codeph"> MediaResource.Type </span>枚举的下列成员之一，对应于指定的文件类型：
      <ul id="ul_C286ED3C31364B858A1C9AF3356E9282">
      <li id="li_25B24EF76D8849DE8764539F25E435FA"> <span class="codeph"> HLS  </span> - M3U8 </li>
      <li id="li_1344A41B434D49229E392F1AAF9ECA81"> <span class="codeph"> ISOBMFF  </span> - ISO基础媒体文件格式(MP4) </li>
      <li id="li_92392073B7334916B06B16570C51AC91"> <span class="codeph"> DASH  </span> - MPEG-DASH媒体演示描述(MPD) </li>
      </ul> </td>
      </tr>
      <tr>
      <td colname="col1"> <span class="codeph"> 元数据  </span> </td>
      <td colname="col2"> <span class="codeph">元数据</span>类（类似字典的结构）的实例，它可能包含有关要加载的内容的其他信息，如要放在主内容中的替代内容或广告内容。 如果使用广告，请在使用此构造函数之前设置<span class="codeph"> AuditudeSettings </span>。 </td>
      </tr>
      </tbody>
   </table>

   >[!IMPORTANT]
   >
   >TVSDK仅支持特定类型的内容的播放。 如果尝试加载任何其他类型的内容，TVSDK将调度错误事件。
   >
   >对于MP4视频点播(VOD)内容，TVSDK不支持特技播放、自适应比特率(ABR)流、广告插入、隐藏式字幕或DRM。

   以下代码创建`MediaResource`实例：

   ```java
   // To do: Create metadata here
   MediaResource res = new MediaResource(
     "https://www.example.com/video/some-video.m3u8",
     MediaResource.Type.HLS,
     metadata);
   ```

   在此步骤之后的任何时间，您都可以使用`MediaResource`访问器(getter)检查资源的类型、URL和元数据。

1. 使用以下选项之一加载媒体资源：

   * MediaPlayer实例。
   * `MediaPlayerItemLoader` 有关详细信息，请 [参阅使用MediaPlayerItemLoader加载媒体资源](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load-using-mediaplayeritemloader.md)。

   >[!IMPORTANT]
   >
   >不要在后台线程上加载媒体资源。 大多数TVSDK操作需要在主线程上运行，而在后台线程上运行这些操作可能会导致操作引发错误并退出。
