---
description: 在使用Primetime DRM Cloud（由ExpressPlay提供支持）时，您可以为Safari启用FairPlay。
title: 为Safari HLS启用FairPlay
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# 为Safari HLS启用FairPlay {#enable-fairplay-for-safari-hls}

在使用Primetime DRM Cloud（由ExpressPlay提供支持）时，您可以为Safari启用FairPlay。

确保您拥有以下权限：

* 可播放HLS视频的功能正常的示例应用程序。

  示例应用程序必须能够播放受FairPlay保护的内容，并通过由ExpressPlay提供支持的Primetime DRM处理许可。
* 与FairPlay保护打包的HLS内容示例（M3U8清单）。

要充分利用此处的信息，请从子部分开始了解多DRM工作流 [参考服务器：示例ExpressPlay授权服务器(SEES)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_multi_drm_workflows.pdf) ，位于多DRM工作流指南。 首先阅读有关如何设置权利和密钥服务器的文档，以下信息将更加有用。
您需要以下项目：

* 您的 *生产* 来自ExpressPlay的客户验证器
* 相同的内容键和 `iv` 用于打包内容的区域。
* FairPlay公钥证书的位置。

要修改FairPlay/Safari应用程序，请执行以下操作：

1. 设置FairPlay许可证服务器请求中使用的FairPlay公钥证书的位置。

   例如：

   ```js
   var myServerCertificatePath = './my_fairplay.cer';
   ```

1. 执行手动Fairplay许可 *令牌* 请求ExpressPlay以获取许可证令牌URL。

       您可以通过以下方式之一完成此步骤：
   
   * 使用您自己的ExpressPlay Production Customer Authenticator。
   * 使用相同的内容密钥和 `iv` 在此请求中用于打包要播放的内容的。

     从shell中运行以下命令并替换ExpressPlay客户身份验证程序以获取示例内容的许可证令牌URL：

     ```
     curl -v "https://fp-gen.service.expressplay.com/hms/fp/token? 
          customerAuthenticator=<ExpressPlay customer authenticator identifier>& 
          errorFormat=json& 
          contentKey=<your content key>& 
          iv=<your iv here>"
     ```

     包含许可证令牌URL的响应将如下所示：

     ```
     https://fp.service.expressplay.com:80/hms/fp/rights/? 
          ExpressPlayToken=<base64-encoded ExpressPlay token>
     ```

1. 使用ExpressPlay中的许可证令牌URL设置变量。

   例如：

   ```js
   var myServerProcessSPCPath = 'https://fp.service.expressplay.com:80/hms/fp/rights/? 
        ExpressPlayToken=<base64-encoded ExpressPlay token>';
   ```

1. 在您的应用程序可以播放受保护的内容之前，请更改内容的URL方案，从 `skd://` 到 `https://`.

   在调用允许播放的许可证服务器之前，您需要在应用程序中添加此URL方案更改。

   协议需要进行更改，因为用于访问密钥管理系统中的内容密钥的内容ID打包到M3U8清单中，其中包含 `skd://` 协议。 当播放器准备好获得播放受保护内容的许可证时，它需要首先切换协议以与ExpressPlay许可证服务器通信。 在以下示例中， `myServerProcessSPCPath` 修改为包含许可证服务器请求的正确URL方案：

   ```js
   extractContentId(initData) {  
       contentId = arrayToString(initData); // contentId is passed up as a URI,  
                                            // from which the host must be extracted:  
       var link = document.createElement('a');  
       link.href = contentId;  
       var index = contentId.indexOf(':');  
       myServerProcessSPCPath = "https:" + contentId.substring(index+1);  
       console.log("severProcessSPCPAth = " + serverProcessSPCPath); return link.hostname;  
   }
   ```
