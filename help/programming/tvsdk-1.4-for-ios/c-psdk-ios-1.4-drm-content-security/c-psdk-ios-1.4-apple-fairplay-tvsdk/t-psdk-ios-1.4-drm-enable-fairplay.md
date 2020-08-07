---
description: 您可以在您的TVSDK应用程序中实施Apple FairPlay流，它是Apple的DRM解决方案。
seo-description: 您可以在您的TVSDK应用程序中实施Apple FairPlay流，它是Apple的DRM解决方案。
seo-title: 在TVSDK应用程序中启用Apple FairPlay
title: 在TVSDK应用程序中启用Apple FairPlay
uuid: fafffdb9-09f9-45fb-9957-3c6e95ed55f9
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---


# 在TVSDK应用程序中启用Apple FairPlay{#enable-apple-fairplay-in-tvsdk-applications}

您可以在您的TVSDK应用程序中实施Apple FairPlay流，它是Apple的DRM解决方案。

1. 通过实施创建FairPlay客户资源加载器 `PTAVAssetResourceLoaderDelegate`。

   有关详细信息，请参 [阅TVSDK应用程序中的Apple FairPlay](../../c-psdk-ios-1.4-drm-content-security/c-psdk-ios-1.4-apple-fairplay-tvsdk/c-psdk-ios-1.4-apple-fairplay-tvsdk.md)。

   >[!NOTE]
   >
   >确保您遵循FairPlay流项目 *指南* (FairPlayStreaming_PG.pdf *)中的说明，该指南包含在*&#x200B;用于开发FPS感知型应用程序的FairPlay Server SDK中 [](https://developer.apple.com/services-account/download?path=/Developer_Tools/FairPlay_Streaming_SDK/FairPlay_Streaming_Server_SDK.zip)。

   该 `resourceLoader:shouldWaitForLoadingOfRequestedResource` 方法等效于中的内容 `AVAssetResourceLoaderDelegate`。

   >[!IMPORTANT]
   >
   >在ExpressPlay许可证服务器场景中，要播放内容，请将ExpressPlay FairPlay服务器许可证请求URL中的URL方案 `skd://` 从更 `https://` 改为 `https://`（或）。

1. 在中注 *册* FairPlay客户资源加载 `registerPTAVAssetResourceLoader`器。

   ```
   PTFairPlayResourceLoader *resourceLoader =  
     [[PTFairPlayResourceLoader new] autorelease];  
   [[PTDefaultMediaPlayerClientFactory defaultFactory]  
     registerPTAVAssetResourceLoader:resourceLoader];
   ```

如果您自行编写了FairPlay许可证服务器，或者您使用的是第三方FairPlay许可证服务器，请咨询许可证服务器供应商以确定许可证服务器URL、格式和任何其他要求。
