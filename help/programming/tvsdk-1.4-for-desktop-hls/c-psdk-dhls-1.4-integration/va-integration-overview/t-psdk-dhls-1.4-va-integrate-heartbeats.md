---
description: 您可以配置播放器以跟踪和分析视频使用情况。
seo-description: 您可以配置播放器以跟踪和分析视频使用情况。
seo-title: 初始化和配置视频分析
title: 初始化和配置视频分析
uuid: ece5ddc1-3f7b-4878-b1bc-1fec0a459add
translation-type: tm+mt
source-git-commit: 6cb3463be8986d8a1dc718655bd929a0f07ac00d
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 0%

---


# 初始化和配置视频分析{#initialize-and-configure-video-analytics}

您可以配置播放器以跟踪和分析视频使用情况。

在激活视频跟踪（视频心跳）之前，请确保您具有以下各项：

* 桌面HLS的TVSDK
* 配置／初始化信息——请与Adobe代表联系以了解您的特定视频跟踪帐户信息：

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84"> 
 <tbody> 
  <tr> 
   <td colname="col1"> AppMeasurement跟踪服务器端点 </td> 
   <td colname="col2"> Adobe Analytics(以前称为SiteCatalyst)后端集合端点的URL。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 视频分析跟踪服务器端点 </td> 
   <td colname="col2"> 视频分析后端集合端点的URL。 这是发送所有视频心跳跟踪调用的位置。 <p>提示： 访客跟踪服务器的URL与分析跟踪服务器的URL相同。 有关实现访客ID服务的信息，请参见<a href="https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-setup-target.html" format="html" scope="external">实现ID服务</a>。 </p> </td> 
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
   <td colname="col1"> 访客跟踪服务器端点 </td> 
   <td colname="col2"> 为当前视频查看器提供唯一标识符的后端端点的URL。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 发布者 </td> 
   <td colname="col2"> 这是发布者ID，由Adobe代表向客户提供。 <p>提示： 此ID不仅是带品牌／电视名称的字符串。 </p> </td> 
  </tr> 
 </tbody> 
</table>

要在播放器中配置视频跟踪，请执行以下操作：

1. 实例化和配置VisitorAPI库。

       请记住以下信息：
   
   * 实例化需要由Marketing Cloud提供的Adobe组织ID输入参数。

      这是字符串值。
   * VisitorAPI库的唯一配置选项是后端端点的URL，该URL为当前用户提供唯一标识符。
   * 访客跟踪服务器的URL与分析跟踪服务器的URL相同。

      有关实现访客ID服务的信息，请参阅访客ID服务实现。

   ```
   var_visitor = new Visitor("MARKETING_CLOUD_ORG_ID"); 
   _visitor.trackingServer = "URL_OF_THE_VISITOR_TRACKER_SERVER”; 
   ```

1. 实例化并配置AppMeasurement组件。

   AppMeasurement实例有许多配置选项。 有关详细信息，请参阅[Adobe Analytics开发人员](https://microsite.omniture.com/t2/help/en_US/reference/#Developer)文档。 以下示例代码（`account`、`visitorNamespace`和`trackingServer`）中的选项是必需的，这些值由Adobe提供。

   >[!IMPORTANT]
   >
   >必须确保正确设置依赖关系链。 AppMeasurement实例聚合（取决于）访客API组件。

   ```
   // Instantiate and configure AppMeasurement 
   
   // Instantiate AppMeasurement instance only once! 
   if (_appMeasurementObject == null) {  
       _appMeasurementObject = new AppMeasurement(); 
   } 
   
   with (_appMeasurementObject) { 
       account = "ACCOUNT_NAME"; // Also known as RSID 
       trackingServer = "URL_OF_THE_ADOBE_ANALYTICS_TRACKING_SERVER"; 
   
       // Use the same value here as for the Visitor API component 
       visitorNamespace = "MARKETING_CLOUD_ORG_ID"; 
   
       // Attach the Visitor API to the AppMeasurement instance. 
       visitor = _visitor;  
       pageName = "pageName"; 
       charSet = "UTF-8"; 
       currencyCode = "USD"; 
   } 
   ```

   >[!IMPORTANT]
   >
   >在您的应用程序中，请确保在启动视频分析流之前填充了`appMeasurementObject.visitor`，否则可能不会得到任何跟踪结果。 这些结果由日志中的消息指示。 您可以添加空的跟踪调用(`appMeasurementObject.track`)，轮询`visitor`属性，直到填充它，然后启动视频分析。

1. 初始化和配置视频心跳跟踪元数据。

   >[!IMPORTANT]
   >
   >您可以停止视频分析模块中间流，并根据需要重新初始化它。 在重新初始化模块之前，请确保视频分析元数据也已更新为正确的内容元数据。 要重新创建元数据，请重复子步骤1和2。

   1. 创建视频分析元数据的实例。

      此实例包含启用视频心跳跟踪所需的所有配置信息。 例如：

      ```
      private function getVideoAnalyticsTrackingMetadata():VideoAnalyticsMetadata {     
          // Initialize visitor id service and appMeasurement      
          [...] // as shown in the previous steps     
      
          var vaMetadata:VideoAnalyticsMetadata = new VideoAnalyticsMetadata(); 
      
          with (vaMetadata) { 
              trackingServer = "hbTrackingServer"; 
              publisher = "hbPublisher"; 
              channel = "hbChannel";  
              playerName = "hbPlayerName"; 
      
              // this overwrites the ContextData variable a.media.friendlyName 
              videoName = "hbFriendlyName";  
      
              // this will overwrite the ContextData variable a.media.name 
              videoId = "hbName"; 
      
              enableChapterTracking = true; 
      
              // Set these to false for production deployment 
              debugLogging = true;  
              quietMode = false; 
      
          } 
      } 
      ```

   1. 将视频分析元数据添加到全局元数据实例。

      准备就绪后，在媒体资源或媒体播放器项目上设置全局元数据实例：

      ```
      var resourceMetadata:Metadata = _player.currentItem.resource.metadata; 
      resourceMetadata.setMetadata(DefaultMetadataKeys.VIDEO_ANALYTICS_METADATA_KEY,  
                                   getVideoAnalyticsTrackingMetadata());
      ```

   1. 初始化视频分析跟踪器。

      创建媒体播放器实例后，必须创建视频分析跟踪器实例并提供对媒体播放器实例的引用。

      >[!TIP]
      >
      >始终为每个内容播放会话创建一个新的跟踪器实例，并在分离媒体播放器实例后删除以前的引用。

      ```
      _videoAnalyticsProvider = new VideoAnalyticsProvider(_appMeasurementObject); 
      _videoAnalyticsProvider.attachMediaPlayer(_player);
      ```

   1. 销毁视频分析跟踪器。

      在开始新的内容播放会话之前，请销毁视频跟踪器的先前实例。 收到内容完成事件（或通知）后，请等待几分钟，然后销毁视频跟踪器实例。 立即销毁该实例可能会干扰视频分析跟踪器发送视频完整ping的能力。

      ```
      if (videoAnalyticsTracker) { 
          videoAnalyticsTracker.detachMediaPlayer(); 
          videoAnalyticsTracker = null; 
      }
      ```

   1. 手动将实时／线性流标记为完成。

      如果您在一个实时流上有各种剧集，则可以使用完整的API手动将剧集标记为完整。 这将结束当前视频集的视频跟踪会话，您可以开始下一集的新跟踪会话。

      >[!TIP]
      >
      >此API是可选的，不是VOD视频跟踪所需的。

