---
title: 使用DRMErrorEvent类概述
description: 使用DRMErrorEvent类概述
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# 使用DRMErrorEvent类 {#using-the-drmerrorevent-class}

Primetime调度 `DRMErrorEvent` Primetime对象在尝试播放受保护内容时遇到 [DRM相关错误](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages). 如果用户凭据无效，则 `DRMAuthenticateEvent` 对象会重复调度，直到用户输入有效凭据或应用程序拒绝进一步尝试为止。 该应用程序负责侦听任何其他DRM错误事件，以检测、识别并处理 [DRM相关错误](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages).

即使使用有效的用户凭据，内容许可证的条款仍会阻止用户查看加密内容。 例如，可以拒绝用户尝试在未经授权的应用程序（例如，应用程序允许列表）中查看内容的访问权限。 未经授权的应用程序是指尚未使用允许列出的应用程序签名证书进行签名的应用程序。 在本例中， `DRMErrorEvent` 对象已调度。

如果内容已损坏或应用程序的版本与许可证指定的版本不匹配，也可以触发错误事件。 应用程序必须提供适当的错误处理机制。

## 创建DRMErrorEvent处理程序 {#create-a-drmerrorevent-handler}

创建事件处理程序，以便在尝试播放受保护内容时遇到错误时处理从Primetime调度的错误事件。

通常，当应用程序遇到错误时，它会执行任意数量的清理任务。 然后通知用户该错误，并提供解决问题的选项。

```
private function drmErrorEventHandler(event:DRMErrorEvent):void {  
    trace(event.toString());  
} 
```
