---
description: 您可以通过将TVSDK与Adobe Analytics集成来跟踪视频使用情况。
seo-description: 您可以通过将TVSDK与Adobe Analytics集成来跟踪视频使用情况。
seo-title: 视频分析
title: 视频分析
uuid: 8f297316-f95e-4896-b489-a2d6b36e6b40
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 视频分析集成 {#video-analytics-integration}

您可以通过将TVSDK与Adobe Analytics集成来跟踪视频使用情况。

TVSDK中的视频跟踪使用 **Adobe Analytics Video Essentials** ，该服务提供视频参与度指标，如视频查看、视频完成、广告印象、视频花费时间等。 有关此服务的详细信息，请与Adobe代表联系。

以下过程总结了在播放器中激活视频跟踪的步骤：

1. 初始化和／或配置以下视频跟踪组件：

   在iOS上，这些组件是TVSDK的一部分：

   * JSON配置文件
   * 视频分析元数据对象
   * 全局元数据对象
   * 视频分析跟踪器对象

1. 使用Adobe Analytics管理工具在服务器端设置视频分析报告。