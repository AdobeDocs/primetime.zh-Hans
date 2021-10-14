---
description: 您可以配置播放器以跟踪和分析视频使用情况。
title: 初始化和配置视频分析
exl-id: 82013882-e314-44fd-82f2-0640575d3c68
source-git-commit: 3bbf70e07b51585c9b53f470180d55aa7ac084bc
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 0%

---

# 初始化和配置视频分析{#initialize-and-configure-video-analytics}

您可以配置播放器以跟踪和分析视频使用情况。

在激活视频跟踪（视频心率）之前，请确保您具有以下功能：

* 适用于Android的TVSDK
* 配置/初始化信息 — 请联系您的Adobe代表，以获取您的特定视频跟踪帐户信息：

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="filepath"> ADBMobileConfig.json  </span> </td> 
   <td colname="col2"> <p>重要信息： 此JSON配置文件名必须保留为<span class="codeph"> ADBMobileConfig.json </span>。 无法更改此配置文件的名称和路径。 此文件的路径必须为<span class="codeph"> &lt;源根&gt;/assets </span>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> AppMeasurement跟踪服务器端点 </td> 
   <td colname="col2"> Adobe Analytics(以前称为SiteCatalyst)后端收集端点的URL。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Video Analytics跟踪服务器端点 </td> 
   <td colname="col2"> Video Analytics后端收集端点的URL。 这是发送所有视频心率跟踪调用的位置。 <p>提示： 访客跟踪服务器的URL与分析跟踪服务器的URL相同。 有关实施访客ID服务的信息，请参阅<a href="https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-target.html?lang=en" format="html" scope="external">实施ID服务</a> 。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 帐户名称 </td> 
   <td colname="col2"> 也称为报表包ID(RSID)。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Marketing Cloud组织ID </td> 
   <td colname="col2"> 实例化访客组件所需的字符串值。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 发布者 </td> 
   <td colname="col2"> 这是发布者ID，由Adobe代表提供给客户。 <p>提示： 此ID不仅是带有品牌/电视名称的字符串。 </p> </td> 
  </tr> 
 </tbody> 
</table>

要在播放器中配置视频跟踪，请执行以下操作：

1. 确认`ADBMobileConfig.json`资源文件中的加载时间选项正确。

   ```
   { 
       "version" : "1.1", 
       "analytics" : { 
           "rsids" : "adobedevelopment", 
           "server" : "10.131.129.149:3000", 
           "charset" : "UTF-8", 
           "ssl" : false, 
           "offlineEnabled" : false, 
           "lifecycleTimeout" : 5, 
           "batchLimit" : 50, 
           "privacyDefault" : "optedin", 
           "poi" : [] 
       }, 
       "marketingCloud": { 
           "org": "ADOBE PROVIDED VALUE"  
       }, 
       "target" : { 
           "clientCode" : "", 
           "timeout" : 5 
       }, 
       "audienceManager" : { 
           "server" : "" 
       } 
   }
   ```

   此JSON格式的配置文件与TVSDK捆绑为资源。 播放器仅在加载时读取这些值，并且这些值在应用程序运行时保持不变。

   要配置加载时间选项，请执行以下操作：

   1. 确认`ADBMobileConfig.json`文件包含由Adobe提供的相应值。
   1. 确认此文件位于`assets`文件夹中。

      此文件夹必须位于应用程序源树的根中。
   1. 编译并构建您的应用程序。
   1. 部署和运行捆绑的应用程序。

      有关这些AppMeasurement设置的更多信息，请参阅[在Adobe Analytics中测量视频](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html?lang=en)。
1. 初始化和配置视频心率跟踪元数据。

   >[!IMPORTANT]
   >
   >您可以停止视频分析模块中间流，并根据需要再次重新初始化它。 在重新初始化模块之前，请确保视频分析元数据也已更新为正确的内容元数据。 要重新创建元数据，请重复执行子步骤1和2。

   1. 创建Video Analytics元数据的实例。

      此实例包含启用视频心率跟踪所需的所有配置信息。 例如：

      ```java
      private VideoAnalyticsMetadata getVideoAnalyticsTrackingMetadata() { 
          VideoAnalyticsMetadata vaMetadata = new VideoAnalyticsMetadata(); 
      
          vaMetadata.setTrackingServer("example.com"); 
          vaMetadata.setPublisher("sample-publisher"); 
          vaMetadata.setChannel("test-channel"); 
          vaMetadata.setVideoName("myvideo"); 
          vaMetadata.setVideoId("myvideoid"); 
          vaMetadata.setPlayerName("PSDK Player"); 
          vaMetadata.setUseSSL(false); 
          vaMetadata.debugLogging = true; // Set to NO for production deployment. 
          vaMetadata.quietMode = false; // Set to NO for production deployment. 
          vaMetadata.setEnableChapterTracking(true); 
          // use this API to override the default asset length -1 for live streams 
          vaMetadata.setAssetDuration(SAMPLE_ASSET_DURATION); 
      
          return vaMetadata; 
      }
      ```

   1. 将Video Analytics元数据添加到全局元数据实例。

      准备就绪后，在媒体资源或媒体播放器项目上设置全局元数据实例：

      ```java
      ((MetadataNode)resourceMetadata).setNode( 
            DefaultMetadataKeys.VIDEO_ANALYTICS_METADATA_KEY.getValue(), vaMetadata);
      ```

   1. 初始化Video Analytics跟踪器。

      创建媒体播放器实例后，必须创建Video Analytics跟踪器实例，并提供对媒体播放器实例的引用。

      >[!TIP]
      >
      >在分离媒体播放器实例后，始终为每个内容播放会话创建新的跟踪器实例，并删除之前的引用。

      ```java
      VideoAnalyticsProvider videoAnalyticsProvider =  
        new VideoAnalyticsProvider(appContext); 
      
      // Attach the TVSDK media player instance 
      videoAnalyticsProvider.attachMediaPlayer(mediaPlayer); 
      ```

   1. 销毁Video Analytics跟踪器。

      在开始新的内容播放会话之前，请销毁视频跟踪器的上一个实例。 收到内容结束事件（或通知）后，请等待几分钟，然后销毁视频跟踪器实例。 立即销毁实例可能会妨碍Video Analytics跟踪器发送视频结束ping的功能。

      ```java
      if (_videoAnalyticsProvider) { 
          _videoAnalyticsProvider.detachMediaPlayer(); 
          _videoAnalyticsProvider = null; 
      }
      ```

   1. 手动将实时/线性流标记为完成。

      如果您在一个实时流上有各种剧集，则可以使用完整的API手动将剧集标记为结束。 这会结束当前视频剧集的视频跟踪会话，并且您可以为下一集启动新的跟踪会话。

      >[!TIP]
      >
      >此API是可选的，VOD视频跟踪不需要此API。

      ```java
      if (_videoAnalyticsProvider) { 
         _videoAnalyticsProvider.trackVideoComplete();    
      }
      ```
