---
description: 浏览器TVSDK存在一些需要注意的安全注意事项。
title: 安全性注意事项
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# 安全性注意事项{#security-considerations}

浏览器TVSDK存在一些需要注意的安全注意事项。

* **AdobeFlash Player**

   * Flash Player不允许访问驻留在SWF发起域之外的数据。

     要允许访问，请在托管数据的服务器的根目录中托管具有适当权限的跨域策略文件。 在FlashTVSDK的浏览器回退模式(Flash Player版本23及更高版本)中，您需要域的授权令牌。 要生成令牌，请联系您的Adobe代表。

* **JavaScript**

   * JavaScript遵循相同的原始策略，并阻止跨域边界访问资源。

     要允许访问这些资源，必须在由播放器以外的源托管的资源上设置Access-Control-Allow-Origin (CORS)标头。 （可选）如果使用字节范围指定内容，则CORS预检选项请求必须指示源允许这些请求。

* **浏览器和混合内容**

   * 浏览器要求通过安全的来源（例如，HTTPS）托管AES-128加密内容。

     由于大多数浏览器不允许混合内容，因此我们建议将播放器、内容和关联的资产（如密钥/WebVTT文件）也托管在安全的原始服务器上。

     >[!IMPORTANT]
     >
     >从版本2.4.5开始，如果播放器通过HTTPS托管，则浏览器TVSDK在使用MSE技术时会将HTTP调用转换为HTTPS。
