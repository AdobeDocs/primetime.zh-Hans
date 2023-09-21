---
description: MediaResource类表示要由MediaPlayer实例加载的内容。
title: 创建媒体资源
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---

# 创建媒体资源 {#create-a-media-resource}

对于每个新视频内容，使用有关视频内容的信息初始化MediaResource实例并加载媒体资源。

MediaResource类表示要由MediaPlayer实例加载的内容。

1. 创建 `MediaResource` 将介质的相关信息传递给 `MediaResource` 构造函数。

   <table id="table_DD0D5D9129D54F73881399B9B4FF546A"> 
    <thead> 
      <tr> 
      <th colname="col1" class="entry"> 构造函数参数 </th> 
      <th colname="col2" class="entry"> 描述 </th> 
      </tr>
    </thead>
    =<tbody> 
      <tr> 
      <td colname="col1"><span class="codeph"> url</span> </td> 
      <td colname="col2"> <p>一个字符串，表示媒体的清单/播放列表的URL。 </p> </td> 
      </tr> 
      <tr> 
      <td colname="col1"><span class="codeph"> type</span> </td> 
      <td colname="col2"> <p>以下对应于所指示文件类型的字符串值之一： 
        <ul id="ul_7512E90B7B294EF9BFBA2D68DE678CBB"> 
        <li id="li_AA84434E84184A3D909552794B425ABD"><span class="codeph"> MP4</span> - ISO基本媒体文件格式(MP4) </li> 
        <li id="li_8A2F3752569344B59EE30303A8393488"><span class="codeph"> HLS</span> - M3U8 </li> 
        </ul> </p> </td> 
      </tr> 
      <tr> 
      <td colname="col1"><span class="codeph"> 元数据</span> </td> 
      <td colname="col2"> <p>的实例 <span class="codeph"> 元数据</span> 类，其中可能包含有关要加载的内容的自定义信息。 </p> <p>内容示例包括要置于主内容中的替换内容或广告内容。 如果使用广告，请设置 <span class="codeph"> Auditudesettings</span> 然后使用此构造函数。 有关更多信息，请参阅 <a href="../../../tvsdk-1.4-for-desktop-hls/ad-insertion/ad-insertion-metadata/c-psdk-dhls-1.4-ad-insertion-metadata.md" format="dita" scope="local"> Ad Insertion元数据</a>. </p> </td> 
      </tr> 
    </tbody> 
   </table>

   >[!IMPORTANT]
   >
   >TVSDK仅支持特定内容类型的播放。 如果您尝试加载任何其他类型的内容，TVSDK会调度错误事件。
   >
   >对于MP4视频点播(VOD)内容，TVSDK不支持特技播放、自适应比特率(ABR)流、广告插入、隐藏式字幕或DRM。

   以下代码创建 `MediaResource` 实例：

   ```
   // To do: Create metadata here
   MyResource = new MediaResource(
            "https://www.example.com/video/some-video.m3u8", 
            "HLS",
            MyMetadata)
   ```

   >[!TIP]
   >
   >此时，您可以使用 `MediaResource` 访问器(getter) ，用于检查资源的类型、URL和元数据。

1. 使用下列方法之一加载媒体资源：

   * MediaPlayer实例。

     有关更多信息，请参阅 [在Mediaplayer中加载媒体资源](../../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-mediaplayer-initialize-for-video/t-psdk-dhls-1.4-media-resource-load.md).
   * A `MediaPlayerItemLoader` 有关更多信息，请参阅 [在Mediaplayer中加载媒体资源](../../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-mediaplayer-initialize-for-video/t-psdk-dhls-1.4-media-resource-load.md).
