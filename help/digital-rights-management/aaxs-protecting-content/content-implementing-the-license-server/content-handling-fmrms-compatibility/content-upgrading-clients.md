---
seo-title: 升级客户端
title: 升级客户端
uuid: 9c9bc7da-2a97-4659-945a-554d778d30a3
translation-type: tm+mt
source-git-commit: 5cf90a75d8805fb64d7d145722ad10a1ce77a14d
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---


# 升级客户端{#upgrading-clients}

如果FMRMS 1.x客户端与Adobe访问服务器联系，则服务器需要提示客户端进行升级。

* 请求处理函数类为`com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`。
* 请求URL为&quot;*来自1.x content*&quot; + &quot;/edcws/services/urn:EDCLicenseService&quot;的基本URL

   与其他Adobe访问请求处理程序不同，此处理程序不提供对任何请求信息的访问，也不要求设置任何响应数据。 创建`FMRMSv1RequestHandler`的实例，然后调用`close()`