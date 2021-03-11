---
description: 您可以在您的TVSDK应用程序中实施Apple FairPlay流，这是Apple的DRM解决方案。
title: 在TVSDK应用程序中启用Apple FairPlay
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---


# 在TVSDK应用程序{#enable-apple-fairplay-in-tvsdk-applications}中启用Apple FairPlay

您可以在您的TVSDK应用程序中实施Apple FairPlay流，这是Apple的DRM解决方案。

1. 通过实施`PTAVAssetResourceLoaderDelegate`创建FairPlay客户资源加载器。

   有关详细信息，请参阅TVSDK应用程序中的[Apple FairPlay](../../c-psdk-ios-1.4-drm-content-security/c-psdk-ios-1.4-apple-fairplay-tvsdk/c-psdk-ios-1.4-apple-fairplay-tvsdk.md)。

   >[!NOTE]
   >
   >确保按照&#x200B;*FairPlay流项目指南*(*FairPlayStreaming_PG.pdf*)中的说明操作，该指南包含在用于开发FPS感知型应用程序的[FairPlay Server SDK中。](https://developer.apple.com/services-account/download?path=/Developer_Tools/FairPlay_Streaming_SDK/FairPlay_Streaming_Server_SDK.zip)

   `resourceLoader:shouldWaitForLoadingOfRequestedResource`方法等效于`AVAssetResourceLoaderDelegate`中的内容。

   >[!IMPORTANT]
   >
   >在ExpressPlay许可证服务器方案中，要播放内容，请将ExpressPlay FairPlay服务器许可证请求URL中的URL方案从`skd://`更改为`https://`（或`https://`）。

1. 使用`registerPTAVAssetResourceLoader`注册&#x200B;*FairPlay*&#x200B;客户资源加载器。

   ```
   PTFairPlayResourceLoader *resourceLoader =  
     [[PTFairPlayResourceLoader new] autorelease];  
   [[PTDefaultMediaPlayerClientFactory defaultFactory]  
     registerPTAVAssetResourceLoader:resourceLoader];
   ```

如果您编写了自己的FairPlay许可证服务器，或者您使用的是第三方FairPlay许可证服务器，请咨询您的许可证服务器供应商以确定您的许可证服务器URL、格式和任何其他要求。
