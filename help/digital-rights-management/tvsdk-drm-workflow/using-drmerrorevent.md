---
title: 使用DRMErrorEvent类概述
description: 使用DRMErrorEvent类概述
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---


# 使用DRMErrorEvent类{#using-the-drmerrorevent-class}

当Primetime对象尝试播放受保护的内容时遇到与DRM相关的错误](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)时，Primetime会调度`DRMErrorEvent`对象。 [如果用户凭据无效，则`DRMAuthenticateEvent`对象会重复调度，直到用户输入有效凭据或应用程序拒绝进一步尝试为止。 应用程序负责侦听任何其他DRM错误事件，以检测、识别和处理与DRM相关的[错误](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)。

即使使用有效的用户凭据，内容的许可证条款仍可能阻止用户查看加密内容。 例如，用户可能因尝试在未经授权的应用程序中视图内容而被拒绝访问（例如，“应用程序允许”列表）。 未授权的应用程序是尚未使用允许列出的应用程序签名证书进行签名的应用程序。 在这种情况下，将调度`DRMErrorEvent`对象。

如果内容已损坏或应用程序的版本与许可指定的版本不匹配，也可触发错误事件。 应用程序必须提供相应的机制来处理错误。

## 创建DRMErrorEvent处理函数{#create-a-drmerrorevent-handler}

创建一个事件处理程序，以处理在尝试播放受保护内容时遇到错误时从Primetime调度的错误事件。

通常，当应用程序遇到错误时，它会执行任意数量的清理任务。 然后，它通知用户该错误并提供解决该问题的选项。

```
private function drmErrorEventHandler(event:DRMErrorEvent):void {  
    trace(event.toString());  
} 
```
