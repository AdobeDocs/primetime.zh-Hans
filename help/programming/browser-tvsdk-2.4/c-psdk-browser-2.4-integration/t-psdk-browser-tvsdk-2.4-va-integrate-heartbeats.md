---
description: 您可以配置播放器以跟踪和分析视频使用情况。
title: 初始化和配置视频分析
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 0%

---


# 初始化和配置视频分析{#initialize-and-configure-video-analytics}

您可以配置播放器以跟踪和分析视频使用情况。

在激活视频跟踪（视频心率）之前，请确保您具有以下功能：

* 配置/浏览器TVSDK初始化信息 — 请联系您的Adobe代表，了解您的特定视频跟踪帐户信息：

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84">
 <tbody>
  <tr>
   <td colname="col1"> AppMeasurement跟踪服务器端点 </td>
   <td colname="col2"> Adobe Analytics(以前为SiteCatalyst)后端集合端点的URL。 </td>
  </tr>
  <tr>
   <td colname="col1"> 视频分析跟踪服务器端点 </td>
   <td colname="col2"> 视频分析后端集合端点的URL。 这是发送所有视频心率跟踪调用的位置。 <p>提示： 访客跟踪服务器的URL与分析跟踪服务器的URL相同。 有关实现访客ID服务的信息，请参阅<a href="https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-setup-target.html" format="html" scope="external">实现ID服务</a>。 </p> </td>
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
   <td colname="col1"> Publisher </td>
   <td colname="col2"> 这是发行商ID，由Adobe代表向客户提供。 <p>提示： 此ID不仅是带有品牌/电视名称的字符串。 </p> </td>
  </tr>
 </tbody>
</table>

要在播放器中配置视频跟踪，请执行以下操作：

1. 实例化并配置VisitorAPI库。

       请记住以下信息：
   
   * 实例化需要由Marketing Cloud提供的Adobe组织ID输入参数。

      这是字符串值。
   * VisitorAPI库的唯一配置选项是提供当前用户唯一标识符的后端端点的URL。
   * 访客跟踪服务器的URL与分析跟踪服务器的URL相同。

      有关实现访客ID服务的信息，请参阅[访客ID服务实现](https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-setup-target.html)。

   ```js
   var_visitor = new Visitor("MARKETING_CLOUD_ORG_ID");
   _visitor.trackingServer = "URL_OF_THE_VISITOR_TRACKER_SERVER”;
   ```

2. 实例化并配置AppMeasurement组件。

   AppMeasurement实例有许多配置选项。 有关详细信息，请访问[Adobe Analytics Developer](https://microsite.omniture.com/t2/help/en_US/reference/#Developer)文档。 以下示例代码（`account`、`visitorNamespace`和`trackingServer`）中的选项是必需的，这些值由Adobe提供。

   >[!IMPORTANT]
   >
   >必须确保正确设置依赖关系链。 AppMeasurement实例聚合（取决于）访客 API组件。

   ```js
   var appMeasurement = new AppMeasurement();
   appMeasurement.visitor = visitor;
   appMeasurement.trackingServer = 'URL_OF_THE_ADOBE_ANALYTICS_TRACKING_SERVER';
   appMeasurement.account = 'ACCOUNT_NAME'; // Also known as RSID
   appMeasurement.pageName = 'Sample Page Name';
   appMeasurement.charSet = "UTF-8";
   appMeasurement.visitorID = "test-vid";
   ```

   >[!IMPORTANT]
   >
   >在您的应用程序中，请确保在启动视频分析流之前填充了`appMeasurementObject.visitor`，否则您可能无法获得任何跟踪结果。 这些结果由日志中的消息指示。 您可以添加空轨道调用(`appMeasurementObject.track`)，轮询`visitor`属性，直到填充它，然后启动视频分析。

3. 初始化和配置视频心率跟踪元数据。

   >[!IMPORTANT]
   >
   >您可以停止视频分析模块中间流，并根据需要重新初始化它。 在重新初始化模块之前，请确保视频分析元数据也已更新为正确的内容元数据。 要重新创建元数据，请重复子步骤1和2。

   1. 创建视频分析元数据的实例。
此实例包含启用视频心率跟踪所需的所有配置信息。 例如：

      ```js
      function getVideoAnalyticsMetadata() {
          var vaObj = new AdobePSDK.VA.VideoAnalyticsMetadata();
          vaObj.appMeasurement = appMeasurement;
          vaObj.trackingServer = 'hbTrackingServer';
          vaObj.publisher = 'hbPublisher';
          vaObj.channel = 'sample-channel';
          vaObj.playerName = 'TVSDK-HTML';
          vaObj.appVersion = '1.0.0';
          vaObj.videoName = 'hbFriendlyName'; // this will overwrite the ContextData variable a.media.friendlyName
          vaObj.assetDuration = durationInSeconds;
          // use this to override the default asset length of -1 for live streams
          vaObj.debugLogging = false;
          return vaObj;
      }
      ```

   2. 创建媒体播放器实例后，创建一个视频分析跟踪器实例并提供对媒体播放器实例的引用。
请记住以下事项：

      * 始终为每个内容播放会话创建新的跟踪器实例，并删除以前的引用（在分离媒体播放器实例后）。
      * 在子步骤1中创建的元数据应在视频分析跟踪器的构造函数中提供。

         ```js
         var videoAnalyticsMetadata = getVideoAnalyticsMetadata();
         videoAnalyticsProvider = new AdobePSDK.VA.VideoAnalyticsProvider(videoAnalyticsMetadata);
         videoAnalyticsProvider.attachMediaPlayer(player);
         ```
   3. 销毁视频分析跟踪器。
在开始新的内容播放会话之前，请销毁视频跟踪器的上一个实例。 收到内容完成事件（或通知）后，请等待几分钟，然后销毁视频跟踪器实例。 立即销毁该实例可能会干扰Video Analytics跟踪器发送视频完整ping的能力。

      ```js
      if (videoAnalyticsProvider) {
          videoAnalyticsProvider.detachMediaPlayer();
          videoAnalyticsProvider = null;
      ```
   4. 手动将实时/线性流标记为完成。
如果您在一个实时流上有各种剧集，则可以使用完整的API手动将某个剧集标记为完整。 这将结束当前视频集的视频跟踪会话，您可以为下一集开始新的跟踪会话。
      >[!TIP]
      >
      >此API是可选的，VOD视频跟踪不需要此API。

      ```js
      if (videoAnalyticsProvider)
      {
         videoAnalyticsProvider.trackVideoComplete();
      videoAnalyticsProvider.detachMediaPlayer();
      videoAnalyticsProvider = null;
      // Create a new instance of VideoAnalyticsProvider to continue tracking.
      } 
      ```
