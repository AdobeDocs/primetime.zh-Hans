---
description: 要在TVSDK应用程序中实施FairPlay流式传输，您需要编写一个资源加载器，该加载器会向FairPlay流式传输服务器发送许可证获取请求。
title: TVSDK应用程序中的Apple FairPlay
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---

# TVSDK应用程序中的Apple FairPlay  {#apple-fairplay-in-tvsdk-applications}

要在TVSDK应用程序中实施FairPlay流式传输，您需要编写一个资源加载器，该加载器会向FairPlay流式传输服务器发送许可证获取请求。

资源加载器代码负责以下任务：

1. 确定许可证获取请求的发送位置。
1. 设置请求的格式。
1. 向服务器提供必要的信息，以便服务器可以决定是否应允许该请求。

例如，如果您使用由ExpressPlay提供支持的AdobePrimetime Cloud DRM，则资源加载器会将请求发送至：

```
https://fp-gen.service.expressplay.com
```

资源加载器会设置请求的格式，并将用于授权播放的ExpressPlay令牌附加到URL。 在获取ExpressPlay令牌时，需要考虑以下几个选项。 这些选项由您打包内容的方式决定。

打包内容时，打包程序将插入 `skd:` M3U8清单中的URL。 在 `skd:` 条目，则可以将任何数据放入清单中。 您可以在应用程序代码中使用此数据来完成上面列出的任务。 例如，您可以使用 `skd:{content_id}` 以便您的应用程序可以确定正在播放的内容的ID，并为该特定内容请求令牌。 例如，您也可以使用 `skd:{entitlement_server_url}?cid={content_id}`，以便您的应用程序无需对授权服务器URL进行硬编码。

您可能不需要在 `skd:` URL — 如果在开始播放时，您已经通过其他渠道知道内容ID。 第二个示例是测试设置的理想解决方案，但您也可以将其用于生产环境。

>[!TIP]
>
>由您决定 `skd:`.

使用获取内容 `skd:` 协议，但您的许可证请求使用 `https:`. 处理这些协议的最常见选项包括：

* **端到端播放的初始测试** 打包内容时，选择 `skd:` URL。 测试应用程序时，从ExpressPlay手动获取许可证并对许可证进行硬编码(在 `https:` URL)和内容URL。

  例如：

  ```
  NSString* const PLAYLIST_URL =  
    @"https://{your_content_URL}/{your_manifest}.m3u8"; 
  NSString* const EXPRESSPLAY_TOKEN =  
    @"https://fp.service.expressplay.com:80/hms/fp/rights/? 
      ExpressPlayToken={copy_your_token_to_here}";
  ```

* **大多数其他案例** 打包内容时，选择 `skd:` 唯一表示内容ID的URL。 在加载器中，解析 `skd:` URL，将其发送到您的服务器以获取令牌，并将生成的令牌用作URL。

  例如：

  ```
  - (BOOL)resourceLoader:(AVAssetResourceLoader *)resourceLoader  
        shouldWaitForLoadingOfRequestedResource:(AVAssetResourceLoadingRequest *)loadingRequest { 
      NSURL *url = [[loadingRequest request] URL]; 
      if (![[url scheme] isEqual:@"skd"]) 
          return NO; 
  
      NSString *strUrl = [url absoluteString]; 
      NSLog(@"url is: %@", strUrl); 
  
      strUrl = [strUrl stringByReplacingOccurrencesOfString:@"skd://" withString:@"https://"]; 
  
      NSData *assetId; 
  
      NSData *requestBytes; 
      NSError* error = nil; 
      BOOL handled = NO; 
  
      NSData  *responseData = nil; 
  
      assetId = getMyAssetIdentifierFromURL(url); 
  
      /* Usecase 1: "On Premise Fairplay Server" 
       * Set the strUrl to the OnPremise Fairplay Server Url. The OnPremise Fairplay  
       * Server Url is either hardcoded in the App or derived from strUrl. 
       */ 
  #if 0  
      // Insert your use case 1 codes here: 
      // strUrl = getOnPremiseServerUrl(strUrl, assetId); 
  #endif // 
  
      /* Usecase 2: The strUrl is the entitlement server. 
       * Send assetId to the entitlement server; if the user is allowed to playback  
       * the content, the entitlement server will send back an ExpressPlay Token Url. 
       */ 
  
  #if 0 
      // The hardcoded SEES server: 
      strUrl = @"https://10.0.248.85:8080/sees/SEESServlet"; 
  
      // You can use the following code to simulate a device binding entitlement  
      // request:  
      // First, invoke getExpressPlayTokenUrlFromEntilementServer with  
      // bEnforceDeviceID set to false. When you play the content, the device_id  
      // will be registered on the ExpressPlay Server.  Now change code to set  
      // bEnforceDeviceID to true, and rerun the program. The ExpressPlay token  
      // sent back by the SEES server will be device bound. 
  
      // The strUrl returned below is the ExpressPlay Token URL. 
      strUrl = getExpressPlayTokenUrlFromEntilementServer(strUrl, assetId, true, &error); 
  #endif 
  
      /* Usecase 3: The strUrl is already the ExpressPlay Token Url. 
       */ 
  
      // Read in the certificate 
      NSLog(@"Get Application Certificate"); 
      NSString* certPath = [[NSBundle mainBundle] pathForResource:@"my_certificate.cer"  
                                                           ofType:nil]; 
  
      NSData *appCert = [NSData dataWithContentsOfFile:certPath]; 
  
      // To create the request blob for the server: 
      requestBytes = [loadingRequest streamingContentKeyRequestDataForApp: appCert 
                                                        contentIdentifier:assetId  
                                                                  options:nil  
                                                                    error:&error]; 
      if (requestBytes == nil) { 
          NSLog(@"Error creating server request: %@", error); 
          return false; 
      } 
      // Per the specification, send requestBytes along with the assetId to the Key 
      // Server and obtain the response. 
      NSError *err; 
  
      responseData = getCKCFromExpressPlayService( strUrl, requestBytes, assetId, &err); 
  
      if (responseData != nil) { 
          NSLog(@"Get response data: "); 
          [loadingRequest finishLoadingWithResponse:nil  
                                               data:(NSData *)responseData 
                                           redirect:nil]; 
      } 
      else { 
          [loadingRequest finishLoadingWithError:err]; 
          NSLog(@"bad key response"); 
      } 
      handled = YES; 
  bail: 
      return handled; 
  
  }
  ```

## 在TVSDK应用程序中启用Apple FairPlay{#enable-apple-fairplay-in-tvsdk-applications}

您可以在TVSDK应用程序中实施Apple FairPlay流(Apple的DRM解决方案)。

1. 通过实施创建FairPlay客户资源加载器 `PTAVAssetResourceLoaderDelegate`.

   有关更多信息，请参阅 [TVSDK应用程序中的Apple FairPlay](../../../tvsdk-1.4-for-ios/c-psdk-ios-1.4-drm-content-security/c-psdk-ios-1.4-apple-fairplay-tvsdk/c-psdk-ios-1.4-apple-fairplay-tvsdk.md).

   >[!NOTE]
   >
   >请确保按照 *FairPlay流媒体节目指南* ( *FairPlayStreaming_PG.pdf*)，包含在 [用于开发FPS感知应用程序的FairPlay Server SDK](https://developer.apple.com/services-account/download?path=/Developer_Tools/FairPlay_Streaming_SDK/FairPlay_Streaming_Server_SDK.zip))。

   此 `resourceLoader:shouldWaitForLoadingOfRequestedResource` 方法等同于中的 `AVAssetResourceLoaderDelegate`.

   >[!IMPORTANT]
   >
   >在ExpressPlay许可证服务器方案中，要播放内容，请将ExpressPlay FairPlay服务器许可证请求URL中的URL方案从 `skd://` 到 `https://` (或 `https://`)。

1. 注册 *公平游戏* 客户资源加载程序具有 `registerPTAVAssetResourceLoader`.

   ```
   PTFairPlayResourceLoader *resourceLoader =  
     [[PTFairPlayResourceLoader new] autorelease];  
   [[PTDefaultMediaPlayerClientFactory defaultFactory]  
     registerPTAVAssetResourceLoader:resourceLoader];
   ```

如果您编写了自己的FairPlay许可证服务器，或者使用的是第三方FairPlay许可证服务器，请咨询您的许可证服务器供应商，以确定您的许可证服务器URL、格式和任何其他要求。
