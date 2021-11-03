---
description: 浏览器TVSDK需要注意一些安全注意事项。
title: 安全注意事项
exl-id: bc98890a-082a-4e2d-b927-ecb3bd878de9
source-git-commit: 78be1575cc7bd6630a7bf85faa061327e5c414d7
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---

# 安全注意事项{#security-considerations}

浏览器TVSDK需要注意一些安全注意事项。

* **AdobeFlash Player**

   * Flash Player不允许访问位于SWF源所在域之外的数据。

      要允许访问，请在托管数据的服务器的根目录中托管具有相应权限的跨域策略文件。 在浏览器TVSDK(Flash Player版本23及更高版本)的Flash回退模式下，您需要域的授权令牌。 要生成令牌，请与您的Adobe代表联系。

* **JavaScript**

   * JavaScript遵循相同的原点策略，并阻止跨域边界访问资源。

      要允许访问这些资源，必须在播放器以外的源上托管的资源上设置访问控制允许源(CORS)标头。 或者，如果内容是使用字节范围指定的，则CORS预检选项请求必须指示源允许这些请求。

* **浏览器和混合内容**

   * 浏览器要求通过安全源（例如，HTTPS）托管AES-128加密内容。

      由于大多数浏览器不允许混合内容，因此我们建议播放器、内容以及关联的资产（如Key/WebVTT文件）也通过安全源进行托管。

      >[!IMPORTANT]
      >
      >从版本2.4.5开始，如果播放器通过HTTPS托管，则浏览器TVSDK在使用MSE技术时会将HTTP调用转换为HTTPS。
