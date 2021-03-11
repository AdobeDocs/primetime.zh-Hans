---
description: 您可以通过将TVSDK与Adobe Analytics集成来跟踪视频使用情况。
title: 视频分析
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# 视频分析{#video-analytics}

您可以通过将TVSDK与Adobe Analytics集成来跟踪视频使用情况。

TVSDK中的视频跟踪使用&#x200B;**Adobe Analytics Video Essentials**&#x200B;服务，该服务提供视频参与度量，如视频视图、视频完成、广告印象、视频逗留时间等。 有关此服务的详细信息，请与Adobe代表联系。

以下过程总结了在播放器中激活视频跟踪的步骤：

1. 初始化和/或配置以下视频跟踪组件：

   * **AppMeasurement库**  — 包含低级数据收集核心逻辑。这是积累视频心率数据并通过网络发送的位置。
   * **视频心率库**  — 包含视频心率数据收集核心逻辑。视频心率库访问`AppMeasurement`库API的子集。

      >[!TIP]
      >
      >您的应用程序不会直接与视频心率代码交互。 相反，应用程序使用TVSDK API配置播放器的视频跟踪功能。

   * **VisitorID库**  — 唯一标识托管视频播放器的网页的访客。
   >[!IMPORTANT]
   >
   >TVSDK内置的视频跟踪功能取决于正确配置的`AppMeasurement`实例。 跟踪元素假定在配置和激活视频跟踪之前，已实例化并配置了`AppMeasurement`库。 TVSDK视频跟踪功能取决于`AppMeasurement`库是否存在一个完全功能且正确配置的实例。

1. 使用Adobe Analytics管理工具在服务器端设置视频分析报告。

