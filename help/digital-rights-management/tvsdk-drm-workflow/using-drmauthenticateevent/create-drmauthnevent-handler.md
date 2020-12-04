---
description: 当Primetime对象尝试播放需要用户凭据才能进行身份验证的受保护内容（且尚未执行身份验证）时，将调度DRMAuthenticateEvent对象。 DRMAuthenticateEvent处理函数负责收集所需的凭据（用户名、密码和类型）并将值传递到。setDRMAuthenticationCredentials()方法进行验证。
seo-description: 当Primetime对象尝试播放需要用户凭据才能进行身份验证的受保护内容（且尚未执行身份验证）时，将调度DRMAuthenticateEvent对象。 DRMAuthenticateEvent处理函数负责收集所需的凭据（用户名、密码和类型）并将值传递到。setDRMAuthenticationCredentials()方法进行验证。
seo-title: 创建DRMAuthenticateEvent处理函数
title: 创建DRMAuthenticateEvent处理函数
uuid: 58330691-d0b5-46bd-9b1d-8dc597580d31
translation-type: tm+mt
source-git-commit: 5749142d42f7d7b36c96592955d1f71f6a7956fc
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---


# 创建DRMAuthenticateEvent处理函数{#create-a-drmauthenticateevent-handler}

当Primetime对象尝试播放需要用户凭据才能进行身份验证的受保护内容（且尚未执行身份验证）时，将调度DRMAuthenticateEvent对象。 DRMAuthenticateEvent处理函数负责收集所需的凭据（用户名、密码和类型）并将值传递到。setDRMAuthenticationCredentials()方法进行验证。

应用程序必须提供一些获取用户凭据的机制。 例如，应用程序可以为用户提供一个简单的用户界面来输入用户名和密码值。 此外，它应提供处理和限制重复身份验证失败尝试的机制。

创建一个事件处理程序，它将一组硬编码的身份验证凭据传递给发起事件的Primetime对象：

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

（此处不包含用于播放视频并确保已成功连接到视频流的代码。）
