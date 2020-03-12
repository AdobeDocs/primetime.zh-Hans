---
description: 您可以在您的TVSDK应用程序中实施Apple FairPlay流，它是Apple的DRM解决方案。
seo-description: 您可以在您的TVSDK应用程序中实施Apple FairPlay流，它是Apple的DRM解决方案。
seo-title: 在TVSDK应用程序中启用Apple FairPlay
title: 在TVSDK应用程序中启用Apple FairPlay
uuid: fafffdb9-09f9-45fb-9957-3c6e95ed55f9
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 在TVSDK应用程序中启用Apple FairPlay{#enable-apple-fairplay-in-tvsdk-applications}

您可以在您的TVSDK应用程序中实施Apple FairPlay流，它是Apple的DRM解决方案。

1. 通过实施创建FairPlay客户资源加载器 `PTAVAssetResourceLoaderDelegate`。

   有关详细信息，请参 [阅TVSDK应用程序中的Apple FairPlay](../../c-psdk-ios-1.4-drm-content-security/c-psdk-ios-1.4-apple-fairplay-tvsdk/c-psdk-ios-1.4-apple-fairplay-tvsdk.md)。

   >[!NOTE]
   >
   >确保按照《 *FairPlay流播放计划指南》(* FairPlayStreaming_PG.pdf *)中的说明进行操作，该指南包含在用于开发FPS感知型应用程序的*[](https://developer.apple.com/services-account/download?path=/Developer_Tools/FairPlay_Streaming_SDK/FairPlay_Streaming_Server_SDK.zip)FairPlay Server SDK中。

   该方 `resourceLoader:shouldWaitForLoadingOfRequestedResource` 法等效于中的内容 `AVAssetResourceLoaderDelegate`。

   >[!IMPORTANT] {importance=&quot;high&quot;}
   >
   >在ExpressPlay许可证服务器场景中，要播放内容，请将ExpressPlay FairPlay服务器许可证请求URL中的URL方案从 `skd://` 更改 `https://` 为(或 `https://`)。

1. 在中注 *册FairPlay* Customer Resource Loader `registerPTAVAssetResourceLoader`。

   ```
   PTFairPlayResourceLoader *resourceLoader =  
     [[PTFairPlayResourceLoader new] autorelease];  
   [[PTDefaultMediaPlayerClientFactory defaultFactory]  
     registerPTAVAssetResourceLoader:resourceLoader];
   ```

如果您自行编写了FairPlay许可证服务器，或者您使用的是第三方FairPlay许可证服务器，请咨询许可证服务器供应商以确定许可证服务器URL、格式和任何其他要求。
