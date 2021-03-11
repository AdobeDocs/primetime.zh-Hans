---
title: 设备组域注册
description: 设备组域注册
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---


# 设备组域注册{#device-group-domain-registration}

作为将许可证绑定到特定设备的替代方法，Adobe Access 3.0和更高版本支持将许可证绑定到设备域。 多个设备可以加入域并接收域令牌。 在域中的设备获得许可证之后，许可证可以被转移到域中的任何其他设备，这些设备可以播放内容而无需直接从许可证服务器获得许可证。

要支持域绑定许可证，策略必须指定客户端必须注册的域服务器。 策略还将指定域服务器的身份验证要求（是否允许匿名访问，或者服务器是否需要用户名/密码或自定义身份验证）。

Adobe访问客户端版本3.0及更高版本支持域注册和域绑定许可证。 如果Flash Player中较旧的客户端或Adobe Access 3.0客户端请求支持域注册的内容的许可证，则许可证服务器可以使用支持绑定到特定设备的替代策略颁发许可证。
