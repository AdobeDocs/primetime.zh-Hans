---
description: 您可以通过将TVSDK与Adobe Analytics集成来跟踪视频使用情况。
title: Video analytics集成
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---

# Video analytics集成 {#video-analytics-integration}

您可以通过将TVSDK与Adobe Analytics集成来跟踪视频使用情况。

TVSDK中的视频跟踪使用 **Adobe Analytics Video Essentials** 服务，用于提供视频参与量度，例如视频查看次数、视频完成次数、广告展示次数、视频逗留时间等。 有关此服务的更多信息，请与您的Adobe代表联系。

以下过程总结了激活播放器中的视频跟踪的步骤：

1. 初始化和/或配置以下视频跟踪组件：

   在iOS上，这些组件是TVSDK的一部分：

   * JSON配置文件
   * 视频分析元数据对象
   * 全局元数据对象
   * 视频分析跟踪器对象

1. 使用Adobe Analytics管理工具在服务器端设置视频分析报表。
