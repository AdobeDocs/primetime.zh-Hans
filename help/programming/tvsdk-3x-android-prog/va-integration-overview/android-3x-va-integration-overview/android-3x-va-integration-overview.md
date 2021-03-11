---
description: 您可以通过将TVSDK与Adobe Analytics集成来跟踪视频使用情况。
title: 将TVSDK与Adobe Analytics集成
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---


# 将TVSDK与Adobe Analytics {#integrating-tvsdk-with-adobe-analytics}集成

您可以通过将TVSDK与Adobe Analytics集成来跟踪视频使用情况。

TVSDK中的视频跟踪使用&#x200B;**Adobe Analytics Video Essentials**&#x200B;服务，该服务提供视频参与度量，如视频视图、视频完成、广告印象、视频逗留时间等。 有关此服务的详细信息，请与Adobe代表联系。

以下过程总结了在播放器中激活视频跟踪的步骤：

1. 初始化和/或配置以下视频跟踪组件：

   >[!TIP]
   >
   >在Android中，这些组件是TVSDK的一部分。

   * JSON配置文件
   * 视频分析元数据对象
   * 全局元数据对象

1. 使用Adobe Analytics管理工具在服务器端设置视频分析报告。