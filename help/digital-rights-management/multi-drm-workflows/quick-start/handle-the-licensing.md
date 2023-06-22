---
description: 许可是允许或拒绝用户播放受保护视频内容的主要机制。 可以向合法（授权）用户颁发许可（密钥），以解密和播放其内容提供商的加密内容的特定片段。
title: 许可
exl-id: 60aa3e77-f821-41b3-ba0e-1a2c05b2bb1a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# 许可{#licensing}

许可是允许或拒绝用户播放受保护视频内容的主要机制。 可以向合法（授权）用户颁发许可（密钥），以解密和播放其内容提供商的加密内容的特定片段。

在最终用户设备上的应用程序或网页可以播放受DRM保护的内容之前，必须从您（客户）运行的授权或店面服务器获取令牌。 Adobe提供了用于此目的的示例参考服务器： [参考服务器：示例ExpressPlay授权服务器(SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md).

您的授权或店面服务器只有在咨询您自己的后端系统以确定特定用户是否有权观看请求的内容后，才会向相关的ExpressPlay服务器请求许可证令牌。 从许可证令牌请求返回的响应是许可证服务器的现成可用URL，或者响应包含采用JSON结构的URL，具体取决于您使用的DRM解决方案。

>[!NOTE]
>
>无法从客户端本身发出许可证令牌请求：
>1. 必须在受信任的环境中检查授权；以及
>1. 客户身份验证器必须保密。


1. 发出许可证令牌请求。

   对于快速入门方案，您只需确保所涉及的各种组件能够协同工作，您可能希望使用 [!DNL curl] 发出许可证令牌请求（而不是最初启动并运行应用程序，然后从那里测试调用）。 例如：

   * Widevine：

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

   请注意，Widevine响应是一个“随时可用”的URL字符串。

   * PlayReady：

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

   请注意，PlayReady响应是一个JSON对象，具有单独的URL和令牌元素。

   * 公平竞争：

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

   请注意，FairPlay响应是一个“随时可用”的URL字符串。
