---
description: 您可以通过将Browser TVSDK与Adobe Analytics集成来跟踪视频使用情况。
title: 视频分析
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# 视频分析{#video-analytics}

您可以通过将Browser TVSDK与Adobe Analytics集成来跟踪视频使用情况。

浏览器TVSDK中的视频跟踪使用 **Adobe Analytics Video Essentials** 服务，用于提供视频参与量度，例如视频查看次数、视频完成次数、广告展示次数、视频逗留时间等。 有关此服务的更多信息，请与您的Adobe代表联系。

以下过程总结了激活播放器中的视频跟踪的步骤：

1. 初始化和/或配置以下视频跟踪组件：

   * **AppMeasurement库**  — 包含低级数据收集核心逻辑。 这是累积视频心率数据并通过网络发送的位置。
   * **视频心率库**  — 包含视频心率数据收集核心逻辑。 视频心率库访问AppMeasurement库API的子集。

     >[!TIP]
     >
     >您的应用程序不会直接与视频心率代码交互。 该应用程序而是使用浏览器TVSDK API来配置播放器的视频跟踪功能。

   * **VisitorID库**  — 唯一标识承载视频播放器的网页的访客。

   >[!IMPORTANT]
   >
   >Browser TVSDK内置的视频跟踪功能取决于正确配置的AppMeasurement实例。 跟踪元素假定在配置和激活视频跟踪之前，已实例化和配置AppMeasurement库。 浏览器TVSDK视频跟踪功能取决于AppMeasurement库是否存在功能齐全且配置正确的实例。

1. 使用Adobe Analytics管理工具在服务器端设置视频分析报表。
