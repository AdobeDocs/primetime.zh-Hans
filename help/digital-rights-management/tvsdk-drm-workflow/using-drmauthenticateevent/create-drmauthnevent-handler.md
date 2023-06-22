---
description: 当Primetime对象尝试播放需要在播放之前进行身份验证的用户凭据（并且尚未执行身份验证）的受保护内容时，将发送DRMAuthenticateEvent对象。 DRMAuthenticationEvent处理程序负责收集所需的凭据（用户名、密码和类型），并将值传递给.setDRMAuthenticationCredentials()方法进行验证。
title: 创建DRMAuthenticateEvent处理程序
exl-id: fe01340b-8a76-4fd4-8c6c-85454d0e2218
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---

# 创建DRMAuthenticateEvent处理程序{#create-a-drmauthenticateevent-handler}

当Primetime对象尝试播放需要在播放之前进行身份验证的用户凭据（并且尚未执行身份验证）的受保护内容时，将发送DRMAuthenticateEvent对象。 DRMAuthenticationEvent处理程序负责收集所需的凭据（用户名、密码和类型），并将值传递给.setDRMAuthenticationCredentials()方法进行验证。

应用程序必须提供某种获取用户凭据的机制。 例如，应用程序可以为用户提供简单的用户界面以输入用户名和密码值。 此外，它还应该提供一种机制，用于处理和限制重复的身份验证失败尝试。

创建一个事件处理程序，该处理程序会将一组硬编码的身份验证凭据传递到发起该事件的Primetime对象：

```
var connection:NetConnection = new NetConnection();  
connection.connect(null);  
var videoStream:Primetime = new Primetime(connection);  
 
videoStream.addEventListener( 
  DRMAuthenticateEvent.DRM_AUTHENTICATE,  
  drmAuthenticateEventHandler)  
  private function drmAuthenticateEventHandler(event:DRMAuthenticateEvent):void {  
    videoStream.setDRMAuthenticationCredentials("administrator", "password", "drm");  
} 
```

（用于播放视频并确保成功连接到视频流的代码未包含在此处。）
