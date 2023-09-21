---
description: MediaResource类表示要由MediaPlayer实例加载的内容。
title: 创建媒体资源
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# 创建媒体资源 {#create-a-media-resource}

MediaResource类表示要由MediaPlayer实例加载的内容。

1. 创建 `MediaResource` 将介质的相关信息传递给 `MediaResource` 构造函数。

   <table id="table_DD0D5D9129D54F73881399B9B4FF546A"> 
    <thead> 
    <tr> 
    <th colname="col1" class="entry"> 构造函数参数 </th> 
    <th colname="col2" class="entry"> 描述 </th> 
    </tr> 
    </thead>
    <tbody> 
    <tr> 
    <td colname="col1"> <p>url </p> </td> 
    <td colname="col2"> <p>一个字符串，表示媒体的清单/播放列表的URL。 </p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>type </p> </td> 
    <td colname="col2"> <p>下列成员之一 <span class="codeph"> MediaResource.Type </span> 对应于所指示文件类型的枚举： </p> <p> 
    <ul id="ul_E9689FA06DC94BF4848F16E1F2F01A59"> 
    <li id="li_83A14B96CDC648C6AF6F5FA745343E1F"> <span class="codeph"> MP4 </span> - ISO基本媒体文件格式(MP4) </li> 
    <li id="li_FCD355151515412D9A78C3815DD09129"> <span class="codeph"> HLS </span> - M3U8 </li> 
    <li id="li_9D3D306D49264830AC6EFB1F49524A3B"> <span class="codeph"> 短划线 </span> - MPD </li> 
    </ul> </p> <p></p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>元数据 </p> </td> 
    <td colname="col2"> <p>的实例 <span class="codeph"> 元数据 </span> 类，其中可能包含有关要加载的内容的自定义信息。 内容示例包括要置于主内容中的替换内容或广告内容。 如果使用广告，请设置 <span class="codeph"> Auditudesettings </span> 然后使用此构造函数。 有关更多信息，请参阅 <a href="../../ad-insertion/ad-insertion-metadata/c-psdk-browser-tvsdk-2.4-ad-insertion-metadata.md">广告插入元数据</a>. </p> <p>Flash提示：如有必要，您可以使用 <span class="codeph"> forceFlash </span> 创建媒体资源时的参数。 这可能很有用，因为浏览器TVSDK当前并非所有功能（例如实时广告工作流）都受支持。 Flash回退用于播放视频内容。 </p> </td> 
    </tr> 
    </tbody> 
   </table>

   >[!IMPORTANT]
   >
   >浏览器TVSDK仅支持播放特定类型的内容。 如果您尝试加载任何其他类型的内容，浏览器TVSDK会调度错误事件。

   以下代码创建 `MediaResource` 实例：

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
   >在此之后的任何时间，您都可以使用 `MediaResource` 访问器(getter) ，用于检查资源的类型、URL和元数据。

1. 加载MediaPlayer实例。 有关更多信息，请参阅 [在MediaPlayer中加载媒体资源](../../content-playback-options-browser-tvsdk/mediaplayer-initialize-for-video/t-psdk-browser-tvsdk-2.4-media-resource-load.md).
