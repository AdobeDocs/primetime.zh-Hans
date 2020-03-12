---
description: MediaResource类表示要由MediaPlayer实例加载的内容。
seo-description: MediaResource类表示要由MediaPlayer实例加载的内容。
seo-title: 创建媒体资源
title: 创建媒体资源
uuid: c25c037e-e9a0-430c-a150-b75a9ac051b1
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 创建媒体资源 {#create-a-media-resource}

MediaResource类表示要由MediaPlayer实例加载的内容。

1. 通过将媒 `MediaResource` 体的相关信息传递给构造函数来创建 `MediaResource` 媒体。

   <table id="table_DD0D5D9129D54F73881399B9B4FF546A"> 
    <thead> 
    <tr> 
    <th colname="col1" class="entry"> 构造函数参数 </th> 
    <th colname="col2" class="entry"> 说明 </th> 
    </tr> 
    </thead>
    <tbody> 
    <tr> 
    <td colname="col1"> <p>url </p> </td> 
    <td colname="col2"> <p>一个字符串，它表示媒体的清单／播放列表的URL。 </p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>type </p> </td> 
    <td colname="col2"> <p>MediaResource.Type枚举的以 <span class="codeph"> 下成员之 </span> 一，该枚举对应于指定的文件类型： </p> <p> 
    <ul id="ul_E9689FA06DC94BF4848F16E1F2F01A59"> 
    <li id="li_83A14B96CDC648C6AF6F5FA745343E1F"> <span class="codeph"> MP4 </span> - ISO基本媒体文件格式(MP4) </li> 
    <li id="li_FCD355151515412D9A78C3815DD09129"> <span class="codeph"> HLS </span> - M3U8 </li> 
    <li id="li_9D3D306D49264830AC6EFB1F49524A3B"> <span class="codeph"> 虚线 </span> - MPD </li> 
    </ul> </p> <p></p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>元数据 </p> </td> 
    <td colname="col2"> <p>Metadata类的一个实 <span class="codeph"> 例， </span> 它可能包含有关要加载的内容的自定义信息。 内容示例是放置在主内容中的替代内容或广告内容。 如果使用广告，请在使用此构 <span class="codeph"> 造函数 </span> 之前设置AuditudeSettings。 有关详细信息，请 <a href="../../ad-insertion/ad-insertion-metadata/c-psdk-browser-tvsdk-2.4-ad-insertion-metadata.md">参阅广告插入元数据</a>。 </p> <p>提示： 如有必要，可以在创建媒体资源时使用 <span class="codeph"> forceFlash </span> 参数强制Flash回退。 这可能很有用，因为浏览器TVSDK当前并不支持所有功能（如实时广告工作流）。 Flash回退用于播放视频内容。 </p> </td> 
    </tr> 
    </tbody> 
   </table>

   >[!IMPORTANT]
   >
   >浏览器TVSDK仅支持特定类型的内容的播放。 如果尝试加载任何其他类型的内容，Browser TVSDK将调度一个错误事件。

   以下代码创建一个 `MediaResource` 实例：

   ```js
   //create a MediaResource instance pointing to some HLS content 
   Metadata metadata = //TODO: create metadata here 
   mediaResource = new AdobePSDK.MediaResource ( 
         "https://www.example.com/video/some-video.m3u8", 
         AdobePSDK.MediaResourceType.HLS,  
         metadata);
   ```

   >[!TIP]
   >
   >此后，您随时可以使用访 `MediaResource` 问器(getter)检查资源的类型、URL和元数据。

1. 加载MediaPlayer实例。 有关详细信息，请 [参阅在MediaPlayer中加载媒体资源](../../content-playback-options-browser-tvsdk/mediaplayer-initialize-for-video/t-psdk-browser-tvsdk-2.4-media-resource-load.md)。
