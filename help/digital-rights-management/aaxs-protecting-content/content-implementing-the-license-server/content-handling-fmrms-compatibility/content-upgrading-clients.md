---
title: 升级客户端
description: 升级客户端
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---


# 升级客户端{#upgrading-clients}

如果FMRMS 1.x客户端与Adobe访问服务器联系，则服务器需要提示客户端进行升级。

* 请求处理程序类为`com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`。
* 请求URL为&quot;*来自1.x content*&quot; + &quot;/edcws/services/urn:EDCLicenseService&quot;的基本URL

   与其他Adobe访问请求处理程序不同，此处理程序不提供对任何请求信息的访问，也不要求设置任何响应数据。 创建`FMRMSv1RequestHandler`的实例，然后调用`close()`