---
description: 您可以通过将Primetime Android参考实施配置为使用您的Adobe Analytics帐户来跟踪视频使用情况。
title: 配置视频分析
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# 配置视频分析 {#configure-video-analytics}

您可以通过将Primetime Android参考实施配置为使用您的Adobe Analytics帐户来跟踪视频使用情况。 Android参考实施旨在将视频使用情况和心率数据发送到Adobe Analytics。 要启用此功能，您必须首先联系Adobe Primetime代表并创建一个Adobe Analytics帐户。

在“参考实施”中，必须配置两个位置才能启用Adobe Analytics集成。 选择要播放的新视频后（即创建新PlayerActivity后），运行时Video Analytics配置会生效。

1. 在中配置加载时间选项 `ADBMobileConfig.json` 资源文件。

   此文件由您的Adobe代表提供。 默认情况下，Primetime SDK包中不包含此变量。 有关此配置文件中设置的更多信息，请参阅此处的Android程序员指南：初始化和配置视频分析。
1. 在“参考实施设置”菜单中配置运行时选项

   ![](assets/img_psdk_ref_impl_va-settings-menu.png)

   | 运行时选项 | 描述 |
   |---|---|
   | Video Analytics跟踪服务器 | Video Analytics后端收集端点的URL。 这是发送所有视频心率跟踪调用的位置。 |
   | 作业ID | 处理作业标识符。 这会向后端端点指示要应用于视频跟踪调用的处理类型。 |
   | 渠道 | 用户从中观看内容的渠道的名称。 对于移动应用程序，这通常是应用程序的名称。 |
   | 发布者 | 内容发布者的名称 |
   | 调试日志记录 | 激活广泛日志记录。 默认情况下处于禁用状态，启用时可能会影响性能，因此您会在生产环境中禁用此功能。 |
   | 安静模式 | 启用此选项后，不会进行网络调用，因此这对于本地调试很有用，但必须禁用它才能用于生产环境。 |
