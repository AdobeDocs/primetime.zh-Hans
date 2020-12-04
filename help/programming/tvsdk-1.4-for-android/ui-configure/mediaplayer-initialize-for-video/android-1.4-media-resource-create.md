---
description: 对于每个新视频内容，使用视频内容的相关信息初始化MediaResource实例并加载媒体资源。 MediaResource类表示要由MediaPlayer实例加载的内容。
seo-description: 对于每个新视频内容，使用视频内容的相关信息初始化MediaResource实例并加载媒体资源。 MediaResource类表示要由MediaPlayer实例加载的内容。
seo-title: 创建媒体资源
title: 创建媒体资源
uuid: d9fe982a-bedf-445c-b5be-f7918693782a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---


# 创建媒体资源{#create-a-media-resource}

对于每个新视频内容，使用视频内容的相关信息初始化MediaResource实例并加载媒体资源。 MediaResource类表示要由MediaPlayer实例加载的内容。

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
    <td colname="col2"> <p><span class="codeph"> MediaResource.Type </span>明细列表的下列成员之一，与指定的文件类型相对应： 
    <ul id="ul_72636C41CA7E4538A3BE11A79E0282FC"> 
    <li id="li_070960200DEB40E992C58FCB8909AEA3"> <span class="codeph"> HLS  </span> - M3U8 </li> 
    </ul> </p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>元数据 </p> </td> 
    <td colname="col2"> <p><span class="codeph">元数据</span>类的实例，其中可能包含有关要加载的内容的自定义信息。 </p> <p>内容的示例是放置在主内容中的替代内容或广告内容。 如果使用广告，请设置<span class="codeph"> AuditudeSettings </span>。 有关详细信息，请参阅<a href="../../../tvsdk-1.4-for-android/ad-insertion/ad-insertion-metadata/android-1.4-ad-insertion-metadata-set-up.md" format="dita" scope="local">Ad Insertion元数据</a>。 </p> </td> 
    </tr> 
    </tbody> 
    </table>

   >[!IMPORTANT]
   >
   >TVSDK仅支持特定类型的内容的播放。 如果尝试加载任何其他类型的内容，TVSDK将发送错误事件。
   >
   >对于MP4视频点播(VOD)内容，TVSDK不支持特技播放、自适应比特率(ABR)流、广告插入、隐藏字幕或DRM。

   以下代码创建`MediaResource`实例：

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
   >此时，您可以使用`MediaResource`访问器(getter)检查资源的类型、URL和元数据。

1. 使用以下方法加载媒体资源：

   * 您的MediaPlayer实例。

      有关详细信息，请参阅[在MediaPlayer](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-resource-load.md)中加载媒体资源。
   * A `MediaPlayerItemLoader`有关详细信息，请参阅[使用MediaPlayerItemLoader](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-mediaplayeritemloader.md)加载媒体资源。
   >[!IMPORTANT]
   >
   >请勿在后台线程上加载媒体资源。 大多数TVSDK操作都需要在主线程上运行，而在后台线程上运行这些操作可能会导致操作抛出错误并退出。
