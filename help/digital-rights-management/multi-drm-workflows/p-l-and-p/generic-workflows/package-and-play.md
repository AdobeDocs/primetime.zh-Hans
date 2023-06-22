---
description: 您可以使用ExpressPlay的Bento4打包程序为Primetime Cloud DRM支持的任何DRM解决方案（由ExpressPlay提供支持）准备内容。
title: ExpressPlay Packager/Cloud DRM/TVSDK
exl-id: ff937279-3866-4d0a-9a19-cf61726299e1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# ExpressPlay Packager/Cloud DRM/TVSDK {#expressplay-packager-cloud-drm-tvsdk}

您可以使用ExpressPlay的Bento4打包程序为Primetime Cloud DRM支持的任何DRM解决方案（由ExpressPlay提供支持）准备内容。

本任务介绍如何使用第三方工具准备受保护的内容，在本例中为 *ExpressPlay Bento4工具*，用于各种DRM解决方案。 欲了解更多信息，请参见 *Bento4工具* 相关文档 [ExpressPlay](https://www.expressplay.com/developer/) 网站。
1. 获取ExpressPlay帐户并获取您的ExpressPlay客户认证信息。

   参见 [Primetime DRM云快速入门。](../../quick-start/quick-overview.md)
1. 如果您正在为Primetime访问加密内容，请从Adobe获取PrimetimeAdobe访问SDK以及所需的证书（许可证、传输和打包证书）。
1. 提供内容加密密钥(CEK)和内容加密密钥存储ID (CEKSID)，以在DRM系统中使用。 （您可以使用OpenSSL或类似工具随机生成这些内容。）

   CEK是您用于加密视频文件的实际密钥。 您可以将其安全地存储在您自己的密钥管理系统中的自己的服务器上，也可以使用ExpressPlay的 [密钥存储解决方案](https://www.expressplay.com/developer/key-storage/).

   CEKSID是特定CEK的标识符。 您（通常）不会传递加密密钥。 例如，在请求许可证令牌时，您提供CEKSID。

1. 如果您正在为Access加密内容，请利用CEK创建与内容关联的Primetime Access元数据。

1. 对内容进行碎片整理，以便 *Bento4 MP4DASH* 工具。

   对于此步骤，您可以使用 *MP4FRAGMENT* 工具。 您只需将内容片段化一次。 例如：

   ```
   ./mp4fragment Unfragmented.mp4 Fragmented.mp4
   ```

1. 使用 *Bento4 MPDASH* 用于“破折号”并加密零碎内容的工具。

   使用此命令指定您将使用的所有DRM系统，并传递从上述步骤生成的任何Primetime访问元数据。 例如：

   ```
   /mp4dash -f  
   --use-segment-list  
   --use-segment-timeline  
   --encryption-key=<CEKSID>:<CEK>  
   --playready  
   --Widevine  
   --Widevine-header=provider:intertrust#content_id:2a  
   --primetime  
   --primetime-metadata=@AAXS.metadata 
    Fragmented.mp4 -o DASH_OUTPUT
   ```

1. 创建“店面服务器”。

       此服务器需要处理以下操作：
   
   1. 客户选择的内容。 此实施需要包含端点，以便客户端请求特定内容ID的内容令牌。
   1. 客户权利
   1. 来自客户端的许可证令牌(ExpressPlay)请求( [ExpressPlay许可证令牌请求/响应引用](../../license-token-req-resp-ref/license-req-resp-overview.md))

1. 创建您的客户端。

   客户端应包括对您的店面服务器的调用。 Adobe建议客户端在用户选择某些内容并经过身份验证后调用店面。 然后，将从ExpressPlay返回的令牌传递给您的播放器，以用于许可证请求。 以下是有关实施播放器的DRM组件的简介：

   * 适用于HTML5的Browser TVSDK
   * [iOS](../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)

1. 有了许可证令牌，客户端现在可以从令牌派生请求URL并向快速播放发出许可证请求，然后为用户播放所选受保护内容。
