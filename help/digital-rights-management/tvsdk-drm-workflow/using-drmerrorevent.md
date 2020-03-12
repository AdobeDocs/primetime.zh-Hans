---
seo-title: 使用DRMErrorEvent类概述
title: 使用DRMErrorEvent类概述
uuid: cbb9c1a7-3c50-479d-b7e5-63010a696dfa
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# 使用DRMErrorEvent类 {#using-the-drmerrorevent-class}

当Primetime对 `DRMErrorEvent` 象尝试播放受保护的内容时，Primetime将调度一个对象，遇到 [DRM相关错误](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)。 如果用户凭据无效，则对象会重复 `DRMAuthenticateEvent` 调度，直到用户输入有效凭据或应用程序拒绝进一步尝试为止。 应用程序负责侦听任何其他DRM错误事件，以检测、识别和处理与 [DRM相关的错误](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)。

即使使用有效的用户凭据，内容的许可条款也仍可能阻止用户查看加密内容。 例如，用户可能因尝试查看未授权应用程序中的内容而被拒绝访问（例如，“应用程序白名单”）。 未授权的应用程序是未用列入白名单的应用程序签名证书进行签名的应用程序。 在这种情况下，将调 `DRMErrorEvent` 度对象。

如果内容损坏或应用程序的版本与许可证指定的版本不匹配，也可以触发错误事件。 应用程序必须提供相应的机制来处理错误。

## 创建DRMErrorEvent处理函数 {#create-a-drmerrorevent-handler}

创建一个事件处理函数，用于处理在尝试播放受保护内容时遇到错误时从Primetime调度的错误事件。

通常，当应用程序遇到错误时，它会执行任意数量的清理任务。 然后，它通知用户该错误并提供解决问题的选项。

```
private function drmErrorEventHandler(event:DRMErrorEvent):void {  
    trace(event.toString());  
} 
```
