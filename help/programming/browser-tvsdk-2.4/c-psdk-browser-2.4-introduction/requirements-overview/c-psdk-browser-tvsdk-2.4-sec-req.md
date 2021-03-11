---
description: 浏览器TVSDK需要注意一些安全注意事项。
title: 安全注意事项
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---


# 安全注意事项{#security-considerations}

浏览器TVSDK需要注意一些安全注意事项。

* **AdobeFlash Player**

   * Flash Player不允许访问位于SWF发源域之外的数据。

      要允许访问，请在承载数据的服务器的根位置托管具有相应权限的跨域策略文件。 在浏览器TVSDK(Flash Player版本23及更高版本)的Flash回退模式下，您需要域的授权令牌。 要生成令牌，请与Adobe代表联系。

* **JavaScript**

   * JavaScript遵循相同的来源策略，并阻止跨域对资源的访问。

      要允许访问这些资源，必须在除播放器之外的来源上托管的资源上设置Access-Control-Allow-来源(CORS)头。 或者，如果内容是通过使用字节范围指定的，则CORS预检选项请求必须指示来源允许这些请求。

* **浏览器和混合内容**

   * 浏览器要求通过安全来源（例如，HTTPS）托管AES-128加密内容。

      由于大多数浏览器不允许混合内容，因此我们建议播放器、内容和相关资源（如Key/WebVTT文件）也通过安全来源托管。

      >[!IMPORTANT]
      >
      >从版本2.4.5开始，如果播放器通过HTTPS托管，则当使用MSE技术时，浏览器TVSDK会将HTTP调用转换为HTTPS。

