---
seo-title: 处理许可证退回请求
title: 处理许可证退回请求
uuid: d184faea-88cb-44f3-a253-e5314d577f17
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---


# 处理许可证退回请求{#handling-license-return-requests}

如果客户端应用程序需要返回许可证，它将调用DRMManager.returnVoucher()Actionscript API来启动该进程。 此API可以在immediateCommit模式或confirmFirst模式下工作。 如果immediateCommit设置为true，客户端将立即删除本地许可证，无需等待许可证服务器确认其已收到返回许可证的请求。 Adobe访问许可证服务器应处理请求并向客户端发送响应。 许可证服务器是否实际执行与请求相关的任何操作（如减少给定用户的许可证数）取决于许可证服务器。

* 请求处理函数类为com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnHandler
* 请求消息类为com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnRequestMessage

所需的最低Adobe访问SDK版本为版本5;请求URL将为“ `/flashaccess/lreturn/v5`”。 与域取消注册一样，服务器应使用`getRequestPhase()`确定客户端是否正在预览许可证返回。
