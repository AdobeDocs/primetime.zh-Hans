---
title: 处理许可证返回请求
description: 处理许可证返回请求
copied-description: true
exl-id: c8813f7a-9a12-4c71-a945-cee73b6784fd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# 处理许可证返回请求{#handling-license-return-requests}

如果客户端应用程序需要返回许可证，它将调用DRMManager.returnVoucher() Actionscript API来启动该过程。 此API可以在immediateCommit模式或confirmFirst模式下工作。 如果immediateCommit设置为true，则客户端将立即删除本地许可证，而不等待许可证服务器确认它已经收到返回许可证的请求。 Adobe访问许可证服务器应处理请求并向客户端发送响应。 许可证服务器是否实际对请求执行任何操作（例如减少给定用户的许可证计数）由许可证服务器决定。

* 请求处理程序类为com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnHandler
* 请求消息类为com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnRequestMessage

所需的最低Adobe访问SDK版本为版本5；请求URL将为&#39;&#39; `/flashaccess/lreturn/v5`“。 与域注销一样，服务器应使用 `getRequestPhase()` 以确定客户端是否正在预览许可证返回。
