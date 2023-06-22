---
title: 处理许可证返回请求
description: 处理许可证返回请求
copied-description: true
exl-id: de577cb9-4ede-440e-8b71-1b39c6cc3c5b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# 处理许可证返回请求{#handle-license-return-requests}

如果客户端应用程序需要返回许可证，它将调用 `DRMManager.returnVoucher()` 用于启动进程的Actionscript API。 此API可在 `immediateCommit` 模式或 `confirmFirst` 模式。 如果 `immediateCommit` 设置为 `true`，则客户端将立即删除本地许可证，而无需等待许可证服务器确认其已收到返回许可证的请求。 Adobe Primetime DRM许可证服务器应处理请求并向客户端发送响应。 许可证服务器是否处理该请求，例如减少指定用户的许可证计数，由许可证服务器决定。

* 请求处理程序类为 `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnHandler`
* 请求消息类为 `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnRequestMessage`

最小值 `Adobe Primetime DRM` 所需的SDK版本为版本5；请求URL为&#39;&#39; [!DNL /flashaccess/lreturn/v5]“。 与域注销一样，服务器使用 `getRequestPhase()` 以确定客户端是否可以预览许可证返回。
