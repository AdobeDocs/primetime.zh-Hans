---
description: 通过将Browser TVSDK与Adobe Analytics集成，您可以跟踪视频使用情况。
title: 视频分析
exl-id: b6fb39a9-6cb8-4498-a9fa-0ea19af52a58
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# 视频分析{#video-analytics}

通过将Browser TVSDK与Adobe Analytics集成，您可以跟踪视频使用情况。

浏览器TVSDK中的视频跟踪使用 **Adobe Analytics Video Essentials** 服务，用于提供视频参与量度，例如视频查看次数、视频完成次数、广告展示次数、视频逗留时间等。 有关此服务的更多信息，请与您的Adobe代表联系。

以下过程总结了激活播放器中的视频跟踪的步骤：

1. 初始化和/或配置以下视频跟踪组件：

   * **AppMeasurement库**  — 包含低级数据收集核心逻辑。 这是通过网络累计和发送视频心率数据的位置。
   * **视频心率库**  — 包含视频心率数据收集核心逻辑。 视频心率库可访问AppMeasurement库API的子集。

      >[!TIP]
      >
      >您的应用程序不会直接与视频心率代码交互。 相反，该应用程序使用浏览器TVSDK API来配置播放器的视频跟踪功能。

   * **VisitorID库**  — 唯一标识托管视频播放器的网页的访客。
   >[!IMPORTANT]
   >
   >浏览器TVSDK内置的视频跟踪功能取决于正确配置的AppMeasurement实例。 跟踪元素假定在配置和激活视频跟踪之前，AppMeasurement库已实例化和配置。 浏览器TVSDK视频跟踪功能取决于AppMeasurement库是否存在功能齐全且配置正确的实例。

1. 使用Adobe Analytics管理工具在服务器端设置视频分析报表。
