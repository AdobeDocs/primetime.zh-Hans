---
description: 当Primetime对象尝试播放在播放之前需要用户凭据进行身份验证的受保护内容（且尚未执行身份验证）时，将调度DRMAuthenticateEvent对象。 DRMAuthenticateEvent处理函数负责收集所需的凭据（用户名、密码和类型）并将值传递到.setDRMAuthenticationCredentials()方法进行验证。
title: 创建DRMAuthenticateEvent处理函数
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# 创建DRMAuthenticateEvent处理函数{#create-a-drmauthenticateevent-handler}

当Primetime对象尝试播放在播放之前需要用户凭据进行身份验证的受保护内容（且尚未执行身份验证）时，将调度DRMAuthenticateEvent对象。 DRMAuthenticateEvent处理函数负责收集所需的凭据（用户名、密码和类型）并将值传递到.setDRMAuthenticationCredentials()方法进行验证。

应用程序必须提供一些获取用户凭据的机制。 例如，应用程序可以为用户提供一个简单的用户界面，以输入用户名和密码值。 此外，它应提供处理和限制重复身份验证失败尝试的机制。

创建一个事件处理函数，它将一组硬编码身份验证凭据传递到发起事件的Primetime对象：

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

（此处不包括用于播放视频并确保已成功连接到视频流的代码。）
