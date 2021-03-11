---
description: 在使用由ExpressPlay提供支持的Primetime DRM Cloud时，您可以启用Fari的FairPlay。
title: 为Safari HLS启用公平播放
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---


# 为Safari HLS {#enable-fairplay-for-safari-hls}启用公平播放

在使用由ExpressPlay提供支持的Primetime DRM Cloud时，您可以启用Fari的FairPlay。

确保您具备以下各项：

* 可播放HLS视频的正常运行范例应用程序。

   范例应用程序必须能够通过ExpressPlay支持的Primetime DRM处理的许可，播放受FairPlay保护的内容。
* 与FairPlay保护一起打包的HLS内容（M3U8清单）示例。

要充分利用此处的信息，请了解从[参考服务器子部分开始的多DRM工作流:多DRM工作流指南中的示例ExpressPlay授权服务器(SEES)](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_multi_drm_workflows.pdf)。 首先阅读关于如何设置您的授权和密钥服务器的文档，下面的信息将更有用。
您需要以下项目：

* 您的&#x200B;*production*&#x200B;来自ExpressPlay的客户身份验证器
* 将内容打包到的内容密钥和`iv`。
* 您的FairPlay公钥证书的位置。

要修改您的FairPlay/Safari应用程序：

1. 设置在FairPlay许可证服务器请求中使用的FairPlay公钥证书的位置。

   例如：

   ```js
   var myServerCertificatePath = './my_fairplay.cer';
   ```

1. 执行手动FairPlay许可证&#x200B;*令牌*&#x200B;请求至ExpressPlay以获取许可证令牌URL。

       您可以通过以下方式之一完成此步骤：
   
   * 使用您自己的ExpressPlay Production Customer Authenticator。
   * 使用此请求中用于打包要播放的内容的相同内容密钥和`iv`。

      从shell中运行以下命令并替换您的ExpressPlay客户身份验证器以获取示例内容的许可证令牌URL:

      ```
      curl -v "https://fp-gen.service.expressplay.com/hms/fp/token? 
           customerAuthenticator=<ExpressPlay customer authenticator identifier>& 
           errorFormat=json& 
           contentKey=<your content key>& 
           iv=<your iv here>"
      ```

      具有许可证令牌URL的响应将如下所示：

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

1. 在应用程序可以播放受保护的内容之前，请将内容的URL方案从`skd://`更改为`https://`。

   在调用允许播放的许可证服务器之前，您需要在应用程序中添加此URL方案更改。

   需要更改这些协议，因为提供对密钥管理系统中内容密钥的访问权限的内容ID使用`skd://`协议打包在M3U8清单中。 当播放器准备好获取许可证以播放受保护的内容时，它需要首先切换协议以与ExpressPlay许可证服务器通信。 在以下示例中，将修改`myServerProcessSPCPath`以包含许可证服务器请求的正确URL方案：

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

