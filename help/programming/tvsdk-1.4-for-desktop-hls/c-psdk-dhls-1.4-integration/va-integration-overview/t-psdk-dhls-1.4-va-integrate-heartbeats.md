---
description: 您可以配置播放器以跟踪和分析视频使用情况。
title: 初始化和配置视频分析
exl-id: 58d560d1-f668-4e1d-a817-b2e02008fdbe
source-git-commit: 3bbf70e07b51585c9b53f470180d55aa7ac084bc
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 0%

---

# 初始化和配置视频分析{#initialize-and-configure-video-analytics}

您可以配置播放器以跟踪和分析视频使用情况。

在激活视频跟踪（视频心率）之前，请确保您满足以下条件：

* 适用于桌面HLS的TVSDK
* 配置/初始化信息 — 请联系您的Adobe代表，以了解特定的视频跟踪帐户信息：

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84"> 
 <tbody> 
  <tr> 
   <td colname="col1"> AppMeasurement跟踪服务器端点 </td> 
   <td colname="col2"> Adobe Analytics(以前的SiteCatalyst)后端收集端点的URL。 </td> 
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
  <tr> 
   <td colname="col1"> 访客跟踪服务器端点 </td> 
   <td colname="col2"> 为当前视频查看器提供唯一标识符的后端端点URL。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 发布者 </td> 
   <td colname="col2"> 这是发布者ID，由客户的Adobe代表提供给客户。 <p>提示：此ID不仅仅是一个带有品牌/电视名称的字符串。 </p> </td> 
  </tr> 
 </tbody> 
</table>

要在播放器中配置视频跟踪，请执行以下操作：

1. 实例化和配置VisitorAPI库。

       请牢记以下信息：
   
   * 实例化需要由Adobe提供的Marketing Cloud组织ID输入参数。

      这是一个字符串值。
   * VisitorAPI库的唯一配置选项是后端端点的URL，它为当前用户提供唯一标识符。
   * 访客跟踪服务器的URL与Analytics跟踪服务器的URL相同。

      有关实施访客ID服务的信息，请参阅访客ID服务实施。

   ```
   var_visitor = new Visitor("MARKETING_CLOUD_ORG_ID"); 
   _visitor.trackingServer = "URL_OF_THE_VISITOR_TRACKER_SERVER”; 
   ```

1. 实例化和配置AppMeasurement组件。

   AppMeasurement实例有许多配置选项。 欲了解更多信息，请参见 [Adobe Analytics开发人员](https://microsite.omniture.com/t2/help/en_US/reference/#Developer) 文档。 以下示例代码中的选项( `account`， `visitorNamespace`、和 `trackingServer`)为必填项，并且值由Adobe提供。

   >[!IMPORTANT]
   >
   >必须确保正确设置依赖关系链。 AppMeasurement实例汇总（取决于）访客API组件。

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
   >在您的应用程序中，确保 `appMeasurementObject.visitor` 会在启动video analytics流之前填充，否则您可能不会获得任何跟踪结果。 这些结果由日志中的消息指示。 您可以添加空跟踪调用( `appMeasurementObject.track`)，轮询 `visitor` 属性，直到被填充，并启动视频分析。

1. 初始化和配置视频心率跟踪元数据。

   >[!IMPORTANT]
   >
   >您可以停止视频分析模块中间流，并在必要时再次重新初始化它。 在重新初始化模块之前，请确保视频分析元数据也已更新为正确的内容元数据。 要重新创建元数据，请重复子步骤1和2。

   1. 创建视频分析元数据的实例。

      此实例包含启用视频心率跟踪所需的所有配置信息。 例如：

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

   1. 将Video Analytics元数据添加到全局元数据实例。

      准备就绪后，在媒体资源或媒体播放器项目上设置全局元数据实例：

      ```
      var resourceMetadata:Metadata = _player.currentItem.resource.metadata; 
      resourceMetadata.setMetadata(DefaultMetadataKeys.VIDEO_ANALYTICS_METADATA_KEY,  
                                   getVideoAnalyticsTrackingMetadata());
      ```

   1. 初始化Video Analytics跟踪器。

      创建媒体播放器实例后，必须创建Video Analytics跟踪器实例，并提供对媒体播放器实例的引用。

      >[!TIP]
      >
      >始终为每个内容播放会话创建新的跟踪器实例，并在分离媒体播放器实例后删除以前的引用。

      ```
      _videoAnalyticsProvider = new VideoAnalyticsProvider(_appMeasurementObject); 
      _videoAnalyticsProvider.attachMediaPlayer(_player);
      ```

   1. 销毁Video Analytics跟踪器。

      在开始新的内容播放会话之前，请销毁视频跟踪器的上一个实例。 收到内容完成事件（或通知）后，请等待几分钟，然后再销毁视频跟踪器实例。 立即销毁实例可能会干扰Video Analytics跟踪器发送视频结束ping的功能。

      ```
      if (videoAnalyticsTracker) { 
          videoAnalyticsTracker.detachMediaPlayer(); 
          videoAnalyticsTracker = null; 
      }
      ```

   1. 手动将实时/线性流标记为完成。

      如果您在一个实时流中有多个剧集，则可以使用完整API手动将剧集标记为完成。 这将结束当前视频集的视频跟踪会话，并且您可以为下一集启动新的跟踪会话。

      >[!TIP]
      >
      >此API是可选的，并且不是VOD视频跟踪所必需的。
