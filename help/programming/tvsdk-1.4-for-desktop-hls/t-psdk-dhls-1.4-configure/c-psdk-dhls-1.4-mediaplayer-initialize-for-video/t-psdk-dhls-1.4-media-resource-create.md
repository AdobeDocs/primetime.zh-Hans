---
description: MediaResource类表示要由MediaPlayer实例加载的内容。
seo-description: MediaResource类表示要由MediaPlayer实例加载的内容。
seo-title: 创建媒体资源
title: 创建媒体资源
uuid: 3d03d92f-69b3-4da8-9b16-25a264115ae5
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# 创建媒体资源 {#create-a-media-resource}

对于每个新的视频内容，使用视频内容的相关信息初始化MediaResource实例并加载媒体资源。

MediaResource类表示要由MediaPlayer实例加载的内容。

1. 通过将媒 `MediaResource` 体的相关信息传递给构造函数来创建 `MediaResource` 媒体。

   <table id="table_DD0D5D9129D54F73881399B9B4FF546A"> 
    <thead> 
      <tr> 
      <th colname="col1" class="entry"> 构造函数参数 </th> 
      <th colname="col2" class="entry"> 说明 </th> 
      </tr>
    </thead>
    =<tbody> 
      <tr> 
      <td colname="col1"><span class="codeph"> url</span> </td> 
      <td colname="col2"> <p>一个字符串，它表示媒体的清单／播放列表的URL。 </p> </td> 
      </tr> 
      <tr> 
      <td colname="col1"><span class="codeph"> type</span> </td> 
      <td colname="col2"> <p>与指示的文件类型相对应的以下字符串值之一： 
        <ul id="ul_7512E90B7B294EF9BFBA2D68DE678CBB"> 
        <li id="li_AA84434E84184A3D909552794B425ABD"><span class="codeph"> MP4</span> - ISO基本媒体文件格式(MP4) </li> 
        <li id="li_8A2F3752569344B59EE30303A8393488"><span class="codeph"> HLS</span> - M3U8 </li> 
        </ul> </p> </td> 
      </tr> 
      <tr> 
      <td colname="col1"><span class="codeph"> 元数据</span> </td> 
      <td colname="col2"> <p>Metadata类的一个实 <span class="codeph"> 例</span> ，它可能包含有关要加载的内容的自定义信息。 </p> <p>内容示例是放置在主内容中的替代内容或广告内容。 如果使用广告，请在使用此构 <span class="codeph"> 造函数之前设置</span> AuditudeSettings。 有关详细信息，请参阅 <a href="../../../tvsdk-1.4-for-desktop-hls/ad-insertion/ad-insertion-metadata/c-psdk-dhls-1.4-ad-insertion-metadata.md" format="dita" scope="local"> 广告插入元数据</a>。 </p> </td> 
      </tr> 
    </tbody> 
   </table>

   >[!IMPORTANT]
   >
   >TVSDK仅支持特定类型的内容的播放。 如果尝试加载任何其他类型的内容，TVSDK将调度错误事件。
   >
   >对于MP4视频点播(VOD)内容，TVSDK不支持特技播放、自适应比特率(ABR)流、广告插入、隐藏式字幕或DRM。

   以下代码创建一个 `MediaResource` 实例：

   ```
   // To do: Create metadata here
   MyResource = new MediaResource(
            "https://www.example.com/video/some-video.m3u8", 
            "HLS",
            MyMetadata)
   ```

   >[!TIP]
   >
   >此时，您可以使用访 `MediaResource` 问器(getter)检查资源的类型、URL和元数据。

1. 使用以下任一方法加载媒体资源：

   * 您的MediaPlayer实例。

      有关详细信息，请 [参阅在Mediaplayer中加载媒体资源](../../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-mediaplayer-initialize-for-video/t-psdk-dhls-1.4-media-resource-load.md)。
   * A有 `MediaPlayerItemLoader` 关详细信息，请参 [阅在Mediaplayer中加载媒体资源](../../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-mediaplayer-initialize-for-video/t-psdk-dhls-1.4-media-resource-load.md)。

