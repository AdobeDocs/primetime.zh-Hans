---
description: 您可以使用ExpressPlay的Bento4打包程序为Premite Cloud DRM支持的任何DRM解决方案准备内容，该解决方案由ExpressPlay提供支持。
seo-description: 您可以使用ExpressPlay的Bento4打包程序为Premite Cloud DRM支持的任何DRM解决方案准备内容，该解决方案由ExpressPlay提供支持。
seo-title: ExpressPlay Packager / Cloud DRM / TVSDK
title: ExpressPlay Packager / Cloud DRM / TVSDK
uuid: 0d2f5a8d-15c4-42ba-acb8-1dc8d5bc62de
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# ExpressPlay Packager / Cloud DRM / TVSDK {#expressplay-packager-cloud-drm-tvsdk}

您可以使用ExpressPlay的Bento4打包程序为Premite Cloud DRM支持的任何DRM解决方案准备内容，该解决方案由ExpressPlay提供支持。

此任务介绍如何使用第三方工具准备受保护的内容(本例中为 *ExpressPlay Bento4 Tools*)，以便与各种DRM解决方案一起使用。 有关其他信息，请参 *阅ExpressPlay网站上的*[](https://www.expressplay.com/developer/) Bento4工具文档。
1. 获取ExpressPlay帐户并获取ExpressPlay客户身份验证器信息。

   请参 [阅Primetime DRM Cloud快速入门。](../../quick-start/quick-overview.md)
1. 如果您正在为Primetime Access加密内容，请从Adobe获得Primetime Adobe Access SDK，并获得所需的证书（许可证、传输和打包证书）。
1. 提供内容加密密钥(CEK)和内容加密密钥存储ID(CEKSID)，以便跨DRM系统使用。 （您使用OpenSSL或类似程序随机生成这些组件。）

   CEK是用于加密视频文件的实际密钥。 您既可以将其安全地存储在您自己的密钥管理系统中自己的服务器上，也可以利用ExpressPlay的密钥存 [储解决方案](https://www.expressplay.com/developer/key-storage/)。

   CEKSID是特定CEK的标识符。 您（通常）不会传递加密密钥。 例如，在请求许可证令牌时，您提供CEKSID。

1. 如果您正在为Access加密内容，请利用您的CEK创建与您的内容相关的Primetime Access元数据。

1. 分段内容，为 *Bento4 MP4DASH工具准备* 。

   对于此步骤，您可以使用 *MP4FRAGMENT工具* 。 您只需将内容分割一次。 例如：

   ```
   ./mp4fragment Unfragmented.mp4 Fragmented.mp4
   ```

1. 使用 *Bento4 MPDASH* 工具“DASH-ify”并加密您的碎片内容。

   使用此命令指定您将使用的所有DRM系统，并传递从前几步生成的任何Primetime Access元数据。 例如：

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
   
   1. 客户选择内容。 此实现需要包括客户端的端点，以便为特定内容ID请求内容令牌。
   1. 客户授权
   1. 来自客户端的许可令牌(ExpressPlay)请求( [ExpressPlay许可令牌请求／响应引用](../../license-token-req-resp-ref/license-req-resp-overview.md))

1. 创建客户。

   客户端应包括对店面服务器的调用。 Adobe建议客户在用户选择某些内容后以及用户通过身份验证后调用店面。 然后，将从ExpressPlay返回的令牌传递给您的播放器以用于许可证请求。 要介绍如何实施播放器的DRM组件，请访问：

   * HTML5浏览器TVSDK
   * [iOS](../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)

1. 有了许可证令牌，客户端现在可以从令牌中派生请求URL并向ExpressPlay发出许可证请求，然后为用户播放选定的受保护内容。
