---
seo-title: 处理许可证退回请求
title: 处理许可证退回请求
uuid: 994df5af-476a-4ee8-b371-8900241be83d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 处理许可证退回请求{#handle-license-return-requests}

如果客户端应用程序需要返回许可证，它将调用 `DRMManager.returnVoucher()` Actionscript API来启动该过程。 此API可以在模式 `immediateCommit` 或模式下工 `confirmFirst` 作。 如果 `immediateCommit` 设置为 `true`，则客户端立即删除本地许可证，而无需等待来自许可证服务器的确认其已收到返回许可证的请求。 Adobe Primetime DRM许可证服务器应处理请求并向客户端发送响应。 许可证服务器是否处理该请求，例如减少指定用户的许可证计数，由许可证服务器决定。

* 请求处理函数类为 `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnHandler`
* 请求消息类为 `com.adobe.flashaccess.sdk.protocol.licensereturn.LicenseReturnRequestMessage`

所需的 `Adobe Primetime DRM` SDK版本最低为版本5;请求URL为“ [!DNL /flashaccess/lreturn/v5]”。 与域取消注册一样，服务器用 `getRequestPhase()` 于确定客户端是否可以预览许可证返回。
