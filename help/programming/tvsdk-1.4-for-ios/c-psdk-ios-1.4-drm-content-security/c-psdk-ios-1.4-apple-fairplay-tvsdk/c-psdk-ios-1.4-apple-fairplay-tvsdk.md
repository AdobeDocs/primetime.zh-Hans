---
description: 要在TVSDK应用程序中实施FairPlay流，您需要编写一个资源加载器，该加载器会向您的FairPlay流服务器发送许可证获取请求。
seo-description: 要在TVSDK应用程序中实施FairPlay流，您需要编写一个资源加载器，该加载器会向您的FairPlay流服务器发送许可证获取请求。
seo-title: TVSDK应用程序中的Apple FairPlay
title: TVSDK应用程序中的Apple FairPlay
uuid: 4384d379-37cd-46c5-8c25-0cda16bdebb8
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 0%

---


# TVSDK应用程序中的Apple FairPlay {#apple-fairplay-in-tvsdk-applications}

要在TVSDK应用程序中实施FairPlay流，您需要编写一个资源加载器，该加载器会向您的FairPlay流服务器发送许可证获取请求。

资源加载器代码负责以下任务:

1. 确定在何处发送许可证获取请求。
1. 格式化请求。
1. 向服务器提供必要的信息，以便服务器能够决定是否允许请求。

例如，如果您使用由ExpressPlay提供支持的Adobe的Primetime Cloud DRM，则您的资源加载器会将请求发送到：

```
https://fp-gen.service.expressplay.com
```

资源加载器设置请求的格式并附加一个ExpressPlay令牌，该令牌授权将播放权放到URL。 获取ExpressPlay令牌时，需考虑几个选项。 这些选项取决于您对内容的打包方式。

在打包内容时，打包程序会在M3U8清单中插入`skd:` URL。 在`skd:`条目之后，可以将任何数据放入清单中。 您可以在应用程序代码中使用此任务完成上面列出的数据。 例如，您可以使用`skd:{content_id}`，这样您的应用程序就可以确定正在播放的内容的ID，并为该特定内容请求令牌。 例如，您也可以使用`skd:{entitlement_server_url}?cid={content_id}`，这样您的应用程序就不需要硬编码授权服务器URL。

如果在播放开始时，您已经通过其他渠道了解内容ID，则您可能不需要`skd:` URL中的任何信息。 第二个示例是测试设置的理想解决方案，但您也可以在生产环境中使用它。

>[!TIP]
>
>确定`skd:`的格式。

您的内容是使用`skd:`协议获取的，但您的许可证请求使用`https:`。 处理这些协议的最常用选项是：

* **端对端回放的初始测试在** 打包内容时，请选择 `skd:` URL。测试应用程序时，请从ExpressPlay手动获取许可证，并在加载器中硬编码许可证(`https:` URL)和内容URL。

   例如：

   ```
   NSString* const PLAYLIST_URL =  
     @"https://{your_content_URL}/{your_manifest}.m3u8"; 
   NSString* const EXPRESSPLAY_TOKEN =  
     @"https://fp.service.expressplay.com:80/hms/fp/rights/? 
       ExpressPlayToken={copy_your_token_to_here}";
   ```

* **大多数其** 他情况打包内容时，请 `skd:` 选择唯一表示内容ID的URL。在加载器中，解析`skd:` URL，将其发送到服务器以获取令牌，然后使用生成的令牌作为URL。

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

您可以在您的TVSDK应用程序中实施Apple FairPlay流，它是Apple的DRM解决方案。

1. 通过实施`PTAVAssetResourceLoaderDelegate`创建FairPlay客户资源加载器。

   有关详细信息，请参阅TVSDK应用程序中的[Apple FairPlay](../../../tvsdk-1.4-for-ios/c-psdk-ios-1.4-drm-content-security/c-psdk-ios-1.4-apple-fairplay-tvsdk/c-psdk-ios-1.4-apple-fairplay-tvsdk.md)。

   >[!NOTE]
   >
   >确保按照&#x200B;*FairPlay流项目指南*(*FairPlayStreaming_PG.pdf*)中的说明进行操作，该指南包含在用于开发FPS感知型应用程序的](https://developer.apple.com/services-account/download?path=/Developer_Tools/FairPlay_Streaming_SDK/FairPlay_Streaming_Server_SDK.zip)[FairPlay服务器SDK中。

   `resourceLoader:shouldWaitForLoadingOfRequestedResource`方法等效于`AVAssetResourceLoaderDelegate`中的内容。

   >[!IMPORTANT]
   >
   >在ExpressPlay许可证服务器场景中，要播放内容，请将ExpressPlay FairPlay服务器许可证请求URL中的URL方案从`skd://`更改为`https://`（或`https://`）。

1. 使用`registerPTAVAssetResourceLoader`注册&#x200B;*FairPlay*&#x200B;客户资源加载器。

   ```
   PTFairPlayResourceLoader *resourceLoader =  
     [[PTFairPlayResourceLoader new] autorelease];  
   [[PTDefaultMediaPlayerClientFactory defaultFactory]  
     registerPTAVAssetResourceLoader:resourceLoader];
   ```

如果您自行编写了FairPlay许可证服务器，或者您使用的是第三方FairPlay许可证服务器，请咨询许可证服务器供应商以确定许可证服务器URL、格式和任何其他要求。