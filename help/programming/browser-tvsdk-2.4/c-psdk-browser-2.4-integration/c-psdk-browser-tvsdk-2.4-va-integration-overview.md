---
description: 您可以通过将浏览器TVSDK与Adobe Analytics集成来跟踪视频使用情况。
seo-description: 您可以通过将浏览器TVSDK与Adobe Analytics集成来跟踪视频使用情况。
seo-title: 视频分析
title: 视频分析
uuid: 6351933b-c0f3-4e3e-ad27-bedc8eecc312
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 视频分析{#video-analytics}

您可以通过将浏览器TVSDK与Adobe Analytics集成来跟踪视频使用情况。

浏览器TVSDK中的视频跟踪使用 **Adobe Analytics Video Essentials** ，该服务提供视频参与度指标，如视频查看、视频完成、广告印象、视频花费时间等。 有关此服务的详细信息，请与Adobe代表联系。

以下过程总结了在播放器中激活视频跟踪的步骤：

1. 初始化和／或配置以下视频跟踪组件：

   * **AppMeasurement库** -包含低级数据收集核心逻辑。 这是通过网络累积和发送视频心跳数据的位置。
   * **视频心跳库** -包含视频心跳数据收集核心逻辑。 视频心跳库访问AppMeasurement库API的子集。

      >[!TIP]
      >
      >您的应用程序不会直接与视频心跳代码交互。 相反，应用程序使用浏览器TVSDK API配置播放器的视频跟踪功能。

   * **VisitorID库** -唯一标识承载视频播放器的网页的访客。
   >[!IMPORTANT]
   >
   >浏览器TVSDK内置的视频跟踪功能取决于正确配置的AppMeasurement实例。 跟踪元素假定在配置和激活视频跟踪之前，AppMeasurement库已实例化和配置。 浏览器TVSDK视频跟踪功能取决于AppMeasurement库是否存在一个完全功能且正确配置的实例。

1. 使用Adobe Analytics管理工具在服务器端设置视频分析报告。