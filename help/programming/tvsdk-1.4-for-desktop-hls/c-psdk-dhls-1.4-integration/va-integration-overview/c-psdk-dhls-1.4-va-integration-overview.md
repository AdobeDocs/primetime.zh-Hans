---
description: 您可以通过将TVSDK与Adobe Analytics集成来跟踪视频使用情况。
seo-description: 您可以通过将TVSDK与Adobe Analytics集成来跟踪视频使用情况。
seo-title: 视频分析
title: 视频分析
uuid: c3cb0574-1117-409c-8aa7-641363d8d85f
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---


# 视频分析{#video-analytics}

您可以通过将TVSDK与Adobe Analytics集成来跟踪视频使用情况。

TVSDK中的视频跟踪使用&#x200B;**Adobe AnalyticsVideo Essentials**&#x200B;服务，该服务提供视频参与度指标，如视频视图、视频完成、广告印象、视频花费时间等。 有关此服务的详细信息，请与Adobe代表联系。

以下过程概括了在播放器中激活视频跟踪的步骤：

1. 初始化和／或配置以下视频跟踪组件：

   * **AppMeasurement库** -包含低级数据收集核心逻辑。这是通过网络累积和发送视频心跳数据的位置。
   * **视频心跳库** -包含视频心跳数据收集核心逻辑。视频心跳库访问`AppMeasurement`库API的子集。

      >[!TIP]
      >
      >您的应用程序不会与视频心跳代码直接交互。 相反，该应用程序使用TVSDK API配置播放器的视频跟踪功能。

   * **访客ID库** -唯一标识托管视频播放器的网页的访客。
   >[!IMPORTANT]
   >
   >TVSDK内置的视频跟踪功能取决于正确配置的`AppMeasurement`实例。 跟踪元素假定在配置和激活视频跟踪之前，`AppMeasurement`库已实例化和配置。 TVSDK视频跟踪功能取决于`AppMeasurement`库是否存在一个完全功能且正确配置的实例。

1. 使用Adobe Analytics管理工具在服务器端设置视频分析报告。

