---
description: 浏览器TVSDK需要注意一些安全注意事项。
seo-description: 浏览器TVSDK需要注意一些安全注意事项。
seo-title: 安全注意事项
title: 安全注意事项
uuid: 78edf2b0-363c-4ab6-b588-ab4748ee6096
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# 安全注意事项{#security-considerations}

浏览器TVSDK需要注意一些安全注意事项。

* **Adobe Flash Player**

   * Flash Player不允许访问位于SWF源所在域之外的数据。

      要允许访问，请在承载数据的服务器的根目录下托管具有相应权限的跨域策略文件。 在浏览器TVSDK（Flash Player版本23及更高版本）的Flash备用模式下，您需要域的授权令牌。 要生成令牌，请与Adobe代表联系。

* **JavaScript**

   * JavaScript遵循相同的源策略并阻止跨域边界访问资源。

      要允许访问这些资源，必须在播放器以外的源上托管的资源上设置Access-Control-Allow-Origin(CORS)头。 或者，如果内容是使用字节范围指定的，则CORS预检选项请求必须指示这些请求由源允许。

* **浏览器和混合内容**

   * 浏览器要求通过安全源（例如，HTTPS）托管AES-128加密内容。

      由于大多数浏览器不允许混合内容，我们建议播放器、内容和关联的资源（如密钥/ WebVTT文件）也通过安全源托管。

      >[!IMPORTANT]
      >
      >从版本2.4.5开始，如果播放器通过HTTPS托管，则浏览器TVSDK在使用MSE技术时将HTTP调用转换为HTTPS。

