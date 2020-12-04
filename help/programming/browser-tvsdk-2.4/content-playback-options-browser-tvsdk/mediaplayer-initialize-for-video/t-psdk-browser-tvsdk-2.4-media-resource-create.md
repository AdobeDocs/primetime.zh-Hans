---
description: MediaResource类表示要由MediaPlayer实例加载的内容。
seo-description: MediaResource类表示要由MediaPlayer实例加载的内容。
seo-title: 创建媒体资源
title: 创建媒体资源
uuid: c25c037e-e9a0-430c-a150-b75a9ac051b1
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---


# 创建媒体资源{#create-a-media-resource}

MediaResource类表示要由MediaPlayer实例加载的内容。

1. 通过将有关媒体的信息传递给`MediaResource`构造函数创建`MediaResource`。

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
    <td colname="col2"> <p>表示媒体清单／播放列表URL的字符串。 </p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>类型 </p> </td> 
    <td colname="col2"> <p><span class="codeph"> MediaResource.Type </span>明细列表的下列成员之一，与指定的文件类型相对应： </p> <p> 
    <ul id="ul_E9689FA06DC94BF4848F16E1F2F01A59"> 
    <li id="li_83A14B96CDC648C6AF6F5FA745343E1F"> <span class="codeph"> MP4  </span> - ISO基础媒体文件格式(MP4) </li> 
    <li id="li_FCD355151515412D9A78C3815DD09129"> <span class="codeph"> HLS  </span> - M3U8 </li> 
    <li id="li_9D3D306D49264830AC6EFB1F49524A3B"> <span class="codeph"> 短划 </span> 线- MPD </li> 
    </ul> </p> <p></p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>元数据 </p> </td> 
    <td colname="col2"> <p><span class="codeph">元数据</span>类的实例，其中可能包含有关要加载的内容的自定义信息。 内容的示例是放置在主内容中的替代内容或广告内容。 如果使用广告，请在使用此构造函数之前设置<span class="codeph"> AuditudeSettings </span>。 有关详细信息，请参阅<a href="../../ad-insertion/ad-insertion-metadata/c-psdk-browser-tvsdk-2.4-ad-insertion-metadata.md">Ad-insertion-metadata</a>。 </p> <p>提示： 如果需要，可以在创建媒体资源时使用<span class="codeph"> forceFlash </span>参数强制Flash回退。 这可能很有用，因为当前并非所有功能(如实时广告工作流)都在浏览器TVSDK中受支持。 Flash回退用于播放视频内容。 </p> </td> 
    </tr> 
    </tbody> 
   </table>

   >[!IMPORTANT]
   >
   >浏览器TVSDK仅支持特定类型的内容的播放。 如果尝试加载任何其他类型的内容，Browser TVSDK将发送错误事件。

   以下代码创建`MediaResource`实例：

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
   >此后，您随时可以使用`MediaResource`访问器(getter)检查资源的类型、URL和元数据。

1. 加载MediaPlayer实例。 有关详细信息，请参阅[在MediaPlayer](../../content-playback-options-browser-tvsdk/mediaplayer-initialize-for-video/t-psdk-browser-tvsdk-2.4-media-resource-load.md)中加载媒体资源。
