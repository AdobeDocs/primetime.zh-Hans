---
title: 缺少设备ID时的无客户端API流
description: 缺少设备ID时的无客户端API流
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# 缺少设备ID时的无客户端API流 {#clientless-api-flow-in-the-absence-of-device-id}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权使用。

</br>


## 问题

并非所有智能设备应用程序都能提供唯一的设备ID。  由于deviceId是必需参数，因此，如果未传递此参数，服务将返回400错误。


## 临时解决方案/解决方法

对于没有设备ID的客户端：

1. 使用首次调用注册代码服务 `deviceId=dummy`
1. 从响应中提取UUID。 UUID在注册代码响应（XML和JSON响应格式）的“id”元素中可用。
1. 再次调用注册服务。 这一次，通过 `deviceId=<uuid obtained in step #2>`
1. 在控制台UI上显示在步骤3中获得的注册码


完成这些步骤后，Adobe Primetime身份验证将使用UUID作为设备ID。 将此设备ID (UUID)存储在设备的本地存储中。 如果用户生成新的注册码，您应再次运行步骤1至4，然后将之前存储的设备ID (UUID)替换为新的设备ID。



## 永久解决方案

Adobe将在未来版本中更改此设置，方法是 `deviceId` 创建注册代码并使用UUID作为令牌键而非时的可选有效负载 `deviceId`，时间 `deviceId` 不存在。

<!--
## Related Information

- [Clientless API Reference](/help/authentication/rest-api-reference.md)
-->
