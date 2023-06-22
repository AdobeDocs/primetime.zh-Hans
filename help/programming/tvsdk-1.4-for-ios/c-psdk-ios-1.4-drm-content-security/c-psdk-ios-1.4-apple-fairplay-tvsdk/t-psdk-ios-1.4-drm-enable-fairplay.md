---
description: 您可以在TVSDK应用程序中实施Apple FairPlay流(Apple的DRM解决方案)。
title: 在TVSDK应用程序中启用Apple FairPlay
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---


# 在TVSDK应用程序中启用Apple FairPlay{#enable-apple-fairplay-in-tvsdk-applications}

您可以在TVSDK应用程序中实施Apple FairPlay流(Apple的DRM解决方案)。

1. 通过实施以下步骤创建FairPlay客户资源加载器 `PTAVAssetResourceLoaderDelegate`.

   有关更多信息，请参阅 [TVSDK应用程序中的Apple FairPlay](../../c-psdk-ios-1.4-drm-content-security/c-psdk-ios-1.4-apple-fairplay-tvsdk/c-psdk-ios-1.4-apple-fairplay-tvsdk.md).

   >[!NOTE]
   >
   >确保按照 *FairPlay流媒体节目指南* ( *FairPlayStreaming_PG.pdf*)，包含在 [用于开发可识别FPS的应用程序的FairPlay Server SDK](https://developer.apple.com/services-account/download?path=/Developer_Tools/FairPlay_Streaming_SDK/FairPlay_Streaming_Server_SDK.zip))。

   此 `resourceLoader:shouldWaitForLoadingOfRequestedResource` 方法等同于 `AVAssetResourceLoaderDelegate`.

   >[!IMPORTANT]
   >
   >在ExpressPlay许可证服务器方案中，要播放内容，请将ExpressPlay FairPlay服务器许可证请求URL中的URL方案从 `skd://` 到 `https://` (或 `https://`)。

1. 注册 *公平竞争* 客户资源加载器，具有 `registerPTAVAssetResourceLoader`.

   ```
   PTFairPlayResourceLoader *resourceLoader =  
     [[PTFairPlayResourceLoader new] autorelease];  
   [[PTDefaultMediaPlayerClientFactory defaultFactory]  
     registerPTAVAssetResourceLoader:resourceLoader];
   ```

如果您自己编写了FairPlay许可证服务器，或者您使用的是第三方FairPlay许可证服务器，请咨询您的许可证服务器供应商，以确定您的许可证服务器URL、格式和任何其他要求。
