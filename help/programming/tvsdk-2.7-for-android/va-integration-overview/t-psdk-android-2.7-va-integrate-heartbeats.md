---
title: 初始化和配置视频分析
description: 初始化和配置视频分析
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# 初始化和配置视频分析 {#initialize-and-configure-video-analytics}

您可以配置播放器以跟踪和分析视频使用情况。
在激活视频跟踪（视频心率）之前，请确保您满足以下条件：

* 适用于Android的TVSDK 2.5。
* 配置/初始化信息

  请联系您的Adobe代表，以了解您的特定视频跟踪帐户信息：

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="filepath"> ADBMobileConfig.json </span> </td> 
   <td colname="col2"> <p>重要信息：必须保留此JSON配置文件名称 <span class="filepath"> ADBMobileConfig.json </span>. 无法更改此配置文件的名称和路径。 此文件的路径必须为 <span class="filepath"> &lt;source root=""&gt;/assets </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> AppMeasurement跟踪服务器端点 </td> 
   <td colname="col2"> Adobe Analytics(以前为SiteCatalyst)后端收集端点的URL。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Video Analytics跟踪服务器端点 </td> 
   <td colname="col2"> Video Analytics后端收集端点的URL。 这是发送所有视频心率跟踪调用的位置。 <p>提示：访客跟踪服务器的URL与Analytics跟踪服务器的URL相同。 有关实施访客ID服务的信息，请参阅 <a href="https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-target.html?lang=en" format="html" scope="external"> 实施ID服务 </a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 帐户名称 </td> 
   <td colname="col2"> 也称为报表包ID (RSID)。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Marketing Cloud组织ID </td> 
   <td colname="col2"> 实例化访客组件所需的字符串值。 </td> 
  </tr> 
 </tbody> 
</table>

要在播放器中配置视频跟踪，请执行以下操作：

1. 确认中的加载时间选项 `ADBMobileConfig.json` 资源文件正确。

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

   此JSON格式配置文件是作为TVSDK资源捆绑在一起的。 您的播放器仅在加载时读取这些值，并且这些值在应用程序运行时保持不变。

   要配置加载时间选项，请执行以下操作：


   1. 确认 `ADBMobileConfig.json` 文件包含相应的值(由Adobe提供)。
   1. 确认此文件位于 `assets/` 文件夹。

      此文件夹必须位于应用程序源树的根目录下。

   1. 编译和构建应用程序。
   1. 部署并运行捆绑的应用程序。

      有关这些AppMeasurement设置的详细信息，请参阅 [在Adobe Analytics中测量视频](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html?lang=en).

1. 初始化和配置视频心率跟踪元数据。

   >[!IMPORTANT]
   >
   >您可以停止视频分析模块中间流，并根据需要再次重新初始化它。 在重新初始化模块之前，请确保将视频分析元数据也更新为正确的内容元数据。 要重新创建元数据，请重复以下前两个步骤（子步骤） **a** 和 **b**)。

   1. 创建视频分析元数据的实例。

      此实例包含启用视频心率跟踪所需的所有配置信息。 例如：

      ```java
      private VideoAnalyticsMetadata getVideoAnalyticsTrackingMetadata() { 
          VideoAnalyticsMetadata vaMetadata = new VideoAnalyticsMetadata(); 
      
          vaMetadata.setTrackingServer("example.com"); 
          vaMetadata.setChannel("test-channel"); 
          vaMetadata.setVideoName("myvideo"); 
          vaMetadata.setVideoId("myvideoid"); 
          vaMetadata.setPlayerName("PSDK Player"); 
          vaMetadata.setUseSSL(false); 
          vaMetadata.debugLogging = true; // Set to NO for production deployment. 
          vaMetadata.setEnableChapterTracking(true); 
          // use this API to override the default asset length -1 for live streams 
          vaMetadata.setAssetDuration(SAMPLE_ASSET_DURATION); 
      
          return vaMetadata; 
      }
      ```

   1. 初始化视频分析提供程序。

      创建媒体播放器实例后，必须创建一个Video Analytics提供程序实例，并为它提供应用程序上下文。

      >[!TIP]
      >
      >始终为每个内容播放会话创建新的提供程序实例，并在分离媒体播放器实例后删除以前的引用。

      ```java
      VideoAnalyticsProvider videoAnalyticsProvider = new VideoAnalyticsProvider(appContext); 
      ```

   1. 在上设置视频分析元数据 `videoAnalyticsProvider` 实例。

      ```java
      videoAnalyticsProvider.setVideoAnalyticsMetadata(vaMetadata);
      ```

   1. 将媒体播放器实例附加到 `videoAnalyticsProvider` 实例：

      ```java
      videoAnalyticsProvider.attachMediaPlayer(mediaPlayer); 
      ```

   1. 销毁Video Analytics提供程序。

      在开始新的内容播放会话之前，请销毁视频提供程序的上一个实例。 收到内容结束事件（或通知）后，请等待几分钟，然后再销毁视频分析提供程序实例。 立即销毁实例可能会妨碍Video Analytics提供程序发送“视频结束”ping的功能。

      ```java
      if (videoAnalyticsProvider) { 
          videoAnalyticsProvider.detachMediaPlayer(); 
          videoAnalyticsProvider = null; 
      }
      ```

   1. 手动将实时/线性流标记为完成。

      如果您在一个实时流上播放了各种剧集，则可以使用完整API手动将剧集标记为完成。 这将结束当前视频集的视频跟踪会话，并且您可以为下一集启动新的跟踪会话。

      >[!TIP]
      >
      >此API是可选的，不适用于VOD视频跟踪。

      ```java
      if (videoAnalyticsProvider) { 
          videoAnalyticsProvider.trackVideoComplete();    
      }
      ```
