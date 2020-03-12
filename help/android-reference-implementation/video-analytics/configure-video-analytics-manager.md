---
description: 您可以通过将Primetime Android参考实施配置为与您的Adobe Analytics帐户一起使用来跟踪视频使用情况。
seo-description: 您可以通过将Primetime Android参考实施配置为与您的Adobe Analytics帐户一起使用来跟踪视频使用情况。
seo-title: 配置视频分析
title: 配置视频分析
uuid: ce2ebab3-b3c8-472a-9c54-16ddb1c3cc4e
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# 配置视频分析 {#configure-video-analytics}

您可以通过将Primetime Android参考实施配置为与您的Adobe Analytics帐户一起使用来跟踪视频使用情况。 Android参考实施旨在将视频使用情况和心跳数据发送到Adobe Analytics。 要启用此功能，您必须先联系Adobe Primetime代表并创建Adobe Analytics帐户。

参考实施中有两个位置，您必须配置它才能启用Adobe Analytics集成。 选择新视频进行回放后，运行时视频分析配置会受到影响（即，创建新的PlayerActivity之后）。

1. 在资产文件中配置加载 `ADBMobileConfig.json` 时间选项。

   此文件由Adobe代表提供。 默认情况下，Primetime SDK包中不包括它。 有关此配置文件中设置的详细信息，请参阅Android程序员指南，网址为：初始化和配置视频分析。
1. 在“参考实施设置”菜单中配置运行时选项

   ![](assets/img_psdk_ref_impl_va-settings-menu.png)

   | 运行时选项 | 说明 |
   |---|---|
   | 视频分析跟踪服务器 | 视频分析后端集合端点的URL。 这是发送所有视频心跳跟踪调用的位置。 |
   | 作业ID | 处理作业标识符。 这向后端端点指示要应用于视频跟踪调用的处理类型。 |
   | 渠道 | 用户观看内容的频道名称。 对于手机应用程序，这通常是应用程序的名称。 |
   | 发布者 | 内容发布者的名称 |
   | 调试日志记录 | 激活大量日志记录。 默认情况下，禁用此选项会在启用时影响性能，因此您对生产环境禁用此选项。 |
   | 安静模式 | 启用此功能后，将不会发出网络调用，因此这对本地调试很有用，但必须对生产环境禁用。 |