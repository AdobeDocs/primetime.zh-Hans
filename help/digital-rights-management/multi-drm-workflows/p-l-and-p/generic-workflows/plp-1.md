---
description: 您可以使用Adobe的Offline Packager为Primetime Cloud DRM支持的任何DRM解决方案（由ExpressPlay提供支持）准备内容。
title: Primetime Packager/Cloud DRM/TVSDK
exl-id: 2055c18b-62de-41bf-9644-f366609e0198
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# Primetime Packager/Cloud DRM/TVSDK {#primetime-packager-cloud-drm-tvsdk}

您可以使用Adobe的Offline Packager为Primetime Cloud DRM支持的任何DRM解决方案（由ExpressPlay提供支持）准备内容。

以下说明假定您已设置ExpressPlay管理员帐户： [Primetime DRM云快速入门](../../../multi-drm-workflows/quick-start/quick-overview.md).
1. 选择用于打包内容的基础架构。 Primetime Packager支持以命令行和基于配置的形式打包内容，以便与FairPlay、Widevine和PlayReady DRM一起使用。 TVSDK当前支持以下格式和加密（管道中提供了更多信息）：

   * DASH (CENC)/PlayReady，Widevine — 用于HTML5
   * HLS/FairPlay、Access — 适用于iOS

1. 选择密钥管理系统(KMS)：

   * 使用ExpressPlay的KMS ( [ExpressPlay密钥存储](https://www.expressplay.com/developer/key-storage/))；此系统通过ExpressPlay的RESTful API管理您的内容密钥。

      或……

   * 设置您自己的KMS。 创建内容键数据库，可通过Content-ID进行选择。

      在任一情况下，KMS管理内容密钥的供应，每个密钥具有相关联的内容ID。

1. 打包您的内容。 借助Primetime Packager，您可以为特定DRM解决方案或多个DRM解决方案打包一段内容。

   以下示例命令显示了针对不同DRM解决方案打包内容的一些示例：

   * [带有Primetime Packager的Widevine](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=19) （生成MPD文件）：

      ```
      java -jar OfflinePackager.jar \ 
        -in_path [ 
        <your_content.mp4>] \ 
        -out_type dash \ 
        -out_path [ 
        <your_out_file_path>] \ 
        -drm \ 
        -drm_sys WIDEVINE \ 
        -key_file_path "creds/widevine_key.bin" \ 
        -widevine_key_id [ 
        <some_keyID>] \ 
        -widevine_content_id [ 
        <some_content-ID] \ 
        -widevine_header provider:intertrust#content_id:2a
      ```

   * [FairPlay与Primetime Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=20) （生成一个M3U8文件）：

      ```
      java -jar OfflinePackager.jar  
        -in_path [ 
        <your_content.mp4>]  
        -out_type hls  
        -out_path [ 
        <your_out_file_path>]  
        -drm  
        -drm_sys FAIRPLAY  
        -key_file_path "creds/fairplay_key.bin"  
        -key_url "user_provided_value"
      ```

      >[!NOTE]
      >
      >此 `key_url` 值将按原样复制到M3U8文件中。

1. 创建“店面服务器”。

       店面服务器需要处理以下操作：
   
   1. 客户选择的内容。 此实施需要包含端点，以便客户端请求特定内容ID的内容令牌。
   1. 客户权利
   1. 来自客户端的许可证令牌(ExpressPlay)请求( [ExpressPlay许可证令牌请求/响应引用](../../../multi-drm-workflows/license-token-req-resp-ref/license-req-resp-overview.md))

1. 创建您的客户端。

       客户端应包括对您的店面服务器的调用。 Adobe建议客户端在用户选择某些内容并经过身份验证后调用店面。 然后，将从ExpressPlay返回的令牌传递给您的播放器，以用于许可证请求。 以下是有关实施播放器的DRM组件的简介：
   
   * [适用于HTML5的Browser TVSDK](https://help.adobe.com/en_US/primetime/psdk/browser_tvsdk/index.html#PSDKs-reference-DRM_interface_overview)
   * [iOS](../../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)

1. 有了许可证令牌，客户端现在可以从令牌派生请求URL并向快速播放发出许可证请求，然后为用户播放选定的内容。
