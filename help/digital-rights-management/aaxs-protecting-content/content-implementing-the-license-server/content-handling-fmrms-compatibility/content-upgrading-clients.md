---
title: 升级客户端
description: 升级客户端
copied-description: true
exl-id: 0476c9ef-3622-4bc5-bb24-f8543470b7d3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---

# 升级客户端{#upgrading-clients}

如果FMRMS 1.x客户端与Adobe访问服务器联系，则服务器需要提示客户端进行升级。

* 请求处理程序类为 `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`.
* 请求URL为&#39;&#39;*来自1.x内容的基本URL*&quot; + &quot;/edcws/services/urn：EDCLicenseService&quot;

   与其他Adobe访问请求处理程序不同，此处理程序不提供对任何请求信息的访问权限，也不要求设置任何响应数据。 创建实例 `FMRMSv1RequestHandler`，然后调用 `close()`
