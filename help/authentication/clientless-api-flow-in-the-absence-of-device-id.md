---
title: 没有设备ID时的无客户端API流
description: 没有设备ID时的无客户端API流
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---


# 没有设备ID时的无客户端API流 {#clientless-api-flow-in-the-absence-of-device-id}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

</br>


## 问题

并非所有智能设备应用程序都能够提供唯一的设备ID。  由于deviceId是必需参数，因此如果未传递，则服务会返回400错误。


## 临时解决方案/解决方法

对于没有设备ID的客户端：

1. 首次使用 `deviceId=dummy`
1. 在响应中，提取UUID。 UUID在注册代码响应的“id”元素（XML和JSON响应格式）中可用。
1. 再次调用注册服务。 这次，通过 `deviceId=<uuid obtained in step #2>`
1. 在控制台UI中显示在步骤3中获取的注册代码


完成这些步骤后，Adobe Primetime身份验证将使用UUID作为设备ID。 将此设备ID(UUID)存储在设备的本地存储中。 如果用户生成了新的注册代码，您应该再次运行步骤1至4，然后将之前存储的设备ID(UUID)替换为新的设备ID。



## 永久解决方案

Adobe将在以后的版本中通过 `deviceId` 创建注册代码并使用UUID作为令牌密钥，而不是 `deviceId`，当 `deviceId` 不存在。

<!--
## Related Information

- [Clientless API Reference](/help/authentication/rest-api-reference.md)
-->