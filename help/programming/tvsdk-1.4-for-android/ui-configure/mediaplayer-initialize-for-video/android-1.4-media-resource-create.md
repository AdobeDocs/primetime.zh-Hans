---
description: 对于每个新视频内容，使用有关视频内容的信息初始化MediaResource实例并加载媒体资源。 MediaResource类表示由MediaPlayer实例加载的内容。
title: 创建媒体资源
exl-id: cda70f91-7f30-4e37-9dfa-888b707e3d61
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# 创建媒体资源 {#create-a-media-resource}

对于每个新视频内容，使用有关视频内容的信息初始化MediaResource实例并加载媒体资源。 MediaResource类表示由MediaPlayer实例加载的内容。

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
    <td colname="col2"> <p>下列成员之一 <span class="codeph"> MediaResource.Type </span> 对应于所指示文件类型的枚举： 
    <ul id="ul_72636C41CA7E4538A3BE11A79E0282FC"> 
    <li id="li_070960200DEB40E992C58FCB8909AEA3"> <span class="codeph"> HLS </span> - M3U8 </li> 
    </ul> </p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>元数据 </p> </td> 
    <td colname="col2"> <p>的实例 <span class="codeph"> 元数据 </span> 类，其中可能包含有关要加载的内容的自定义信息。 </p> <p>内容示例为要放置在主内容中的替换内容或广告内容。 如果使用广告，请设置 <span class="codeph"> Auditudesettings </span>. 有关更多信息，请参阅 <a href="../../../tvsdk-1.4-for-android/ad-insertion/ad-insertion-metadata/android-1.4-ad-insertion-metadata-set-up.md" format="dita" scope="local"> Ad Insertion元数据 </a>. </p> </td> 
    </tr> 
    </tbody> 
    </table>

   >[!IMPORTANT]
   >
   >TVSDK仅支持播放特定类型的内容。 如果您尝试加载任何其他类型的内容，TVSDK会调度一个错误事件。
   >
   >对于MP4视频点播(VOD)内容，TVSDK不支持特技播放、自适应比特率(ABR)流、广告插入、隐藏式字幕或DRM。

   以下代码创建 `MediaResource` 实例：

   ```java
   try { 
       // create a MediaResource instance pointing to some HLS content 
       Metadata metadata = //TODO: create metadata  
       MediaResource mediaResource = MediaResource.createFromUrl( 
         "https://www.example.com/video/some-video.m3u8",  
         MediaResource.Type.HLS,  
         metadata); 
   } catch(IllegalArgumentException ex) { 
       // this exception is thrown if the URL does not point  
       // to a valid url. 
   } 
   ```

   >[!TIP]
   >
   >此时，您可以使用 `MediaResource` 访问器(getter) ，用于检查资源的类型、URL和元数据。

1. 使用以下方式加载媒体资源：

   * MediaPlayer实例。

      有关更多信息，请参阅 [在MediaPlayer中加载媒体资源](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-resource-load.md).
   * A `MediaPlayerItemLoader` 有关更多信息，请参阅 [使用MediaPlayerItemLoader加载媒体资源](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-mediaplayeritemloader.md).
   >[!IMPORTANT]
   >
   >请勿在后台线程上加载媒体资源。 大多数TVSDK操作需要在主线程上运行，而在后台线程上运行这些操作可能会导致操作抛出错误并退出。
