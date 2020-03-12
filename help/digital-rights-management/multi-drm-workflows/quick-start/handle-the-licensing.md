---
description: 许可是允许用户播放一段受保护视频内容或拒绝用户播放该内容的主要机制。 合法（已授权）用户可以获得许可证（密钥）以解密和播放其内容提供商的加密内容的特定片段。
seo-description: 许可是允许用户播放一段受保护视频内容或拒绝用户播放该内容的主要机制。 合法（已授权）用户可以获得许可证（密钥）以解密和播放其内容提供商的加密内容的特定片段。
seo-title: 许可
title: 许可
uuid: 9f433d62-5609-4d88-95fd-c1e7c0f6aa75
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 许可{#licensing}

许可是允许用户播放一段受保护视频内容或拒绝用户播放该内容的主要机制。 合法（已授权）用户可以获得许可证（密钥）以解密和播放其内容提供商的加密内容的特定片段。

在最终用户设备上的应用程序或网页播放受DRM保护的内容之前，它必须从您（客户）操作的授权或店面服务器获取令牌。 Adobe为此提供示例参考服务器：参 [考服务器：示例ExpressPlay授权服务器(SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md)。

您的授权或店面服务器只有在与您自己的后端系统核对之后，才会从相关的ExpressPlay服务器请求许可证令牌，以确定特定用户是否有权观看所请求的内容。 从许可令牌请求返回的响应是许可证服务器的可用URL，或者响应包含JSON结构中的URL，具体取决于您使用的DRM解决方案。

>[!NOTE]
>
>无法从客户端本身发出许可证令牌请求：
>1. 授权必须在可信环境中进行检查；和
>1. 客户身份验证器必须保密。


1. 发出许可证令牌请求。

   对于快速启动方案，您只希望确保所涉及的各个组件协同工作，您可能希望使用类似的方式发出许可证令牌请求（与最初启动应用程序并从那里运行和测试调用相反）。 [!DNL curl] 例如：

   * Widevine:

   ```
   curl "https://wv-gen.test.expressplay.com/hms/wv/token?customerAuthenticator= 
   <Customer Authenticator> 
   &kid 
   <indexterm>
   CEKSID 
     <indexterm>
     as query parameter kid 
    <indexterm>
    Widevine 
    </indexterm> 
    </indexterm> 
    </indexterm>=<CEKSID> 
      &contentKey 
    <indexterm>
    CEK 
    <indexterm>
    as query parameter contentKey 
    <indexterm>
    Widevine 
    </indexterm> 
    </indexterm> 
    </indexterm>=<CEK> 
      &<Any additional licensing attributes desired>" >>WidevineToken 
   ```

   示例Widevine测试令牌：

   ```
   https://wv.test.expressplay.com/widevine/RightsManager.asmx?ExpressPlayToken= 
      AQAAAJJ2Y0MAAABQbyvnJ6KgEg_w-2yZmU-MsjTEZ3f7UkhUcFhDFAvdonzBk 
      RGQU-xe1G-DMbel5-BVH_PozovdWhKZx0_SXRokfh9-FERmBl6OEfGfPqMI1e 
      O1PqRkx59Q2q1s2cFNrqfml8Y3RQ 
   ```

   请注意，Widevine响应是“就绪”URL字符串。

   * 播放就绪：

   ```
   curl "https://pr-gen.test.expressplay.com/hms/pr/token?customerAuthenticator= 
   <Customer Authenticator> 
      &kid 
   <indexterm>
   CEKSID 
   <indexterm>
   as query parameter kid 
   <indexterm>
    PlayReady 
   </indexterm> 
   </indexterm> 
   </indexterm>=<Key ID> 
      &contentKey 
   <indexterm>
    CEK 
    <indexterm>
    as query parameter contentKey 
    <indexterm>
    PlayReady 
   </indexterm> 
   </indexterm> 
   </indexterm>=<CEK> 
      &<Any additional licensing attributes desired>" >>playreadyToken
   ```

   示例PlayReady测试令牌：

   ```
   {"licenseAcquisitionUrl":"https://pr.test.expressplay.com/playready/RightsManager.asmx", 
   "token":"AQAAAxBbWv4AAABgV8_GaWjU80mObLQdfwEdy1lenXmcqvx5VLyqixigtwXLthzjPxq9QDT-TYbudNrMSOpUAy 
   G_2Qt8RdTGJ2_Q_xtRfnj7H6C-yt6By40IhNaSQ0nNYUsY1_MtCrHXIltlVhN2Ekr_RNyTNvCjYs0V5TqzOPY"} 
   ```

   请注意，PlayReady响应是一个JSON对象，带有单独的URL和令牌元素。

   * FairPlay:

   ```
   curl "https://fp-gen.test.expressplay.com/hms/fp/token?customerAuthenticator= 
    <Customer Authenticator> 
    &kid 
    <indexterm>
      CEKSID 
    <indexterm>
      as query parameter kid 
      <indexterm>
        FairPlay 
      </indexterm> 
    </indexterm> 
    </indexterm>=<Key ID> 
          &contentKey 
    <indexterm>
      CEK 
    <indexterm>
      as query parameter contentKey 
      <indexterm>
        FairPlay 
      </indexterm> 
    </indexterm> 
    </indexterm>=<CEK> 
    &iv=<IV ID> 
    &<Any additional licensing attributes desired>"
   ```

   示例FairPlay测试令牌：

   ```
   https://{expressplay_test_domain_license_url}/?ExpressPlayToken= 
   AQAAAJJ2Y0MAAABQbyvnJ6KgEg_w-2yZmU-MsjTEZ3f7UkhUcFhDFAvdonzBk 
   RGQU-xe1G-DMbel5-BVH_PozovdWhKZx0_SXRokfh9-FERmBl6OEfGfPqMI1e 
   O1PqRkx59Q2q1s2cFNrqfml8Y3RQ
   ```

   请注意，FairPlay响应是一个“即用”URL字符串。
