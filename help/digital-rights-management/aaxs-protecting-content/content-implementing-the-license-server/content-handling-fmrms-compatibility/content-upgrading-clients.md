---
seo-title: 升级客户端
title: 升级客户端
uuid: 9c9bc7da-2a97-4659-945a-554d778d30a3
translation-type: tm+mt
source-git-commit: 5cf90a75d8805fb64d7d145722ad10a1ce77a14d

---


# 升级客户端{#upgrading-clients}

如果FMRMS 1.x客户端与Adobe Access服务器联系，则服务器需要提示客户端进行升级。

* 请求处理程序类是 `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`。
* 请求URL是“*1.x content*” + &quot;/edcws/services/urn:EDCLicenseService的基本URL”

   与其他Adobe Access请求处理程序不同，此处理程序不提供对任何请求信息的访问，也不要求设置任何响应数据。 创建实例 `FMRMSv1RequestHandler`，然后调用 `close()`