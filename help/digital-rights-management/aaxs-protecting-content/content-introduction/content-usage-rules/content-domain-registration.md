---
title: 设备组域注册
description: 设备组域注册
copied-description: true
exl-id: 1f3e9d26-c185-4d12-accf-aa74a313f890
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# 设备组域注册{#device-group-domain-registration}

作为将许可证绑定到特定设备的替代方法，Adobe访问3.0及更高版本支持将许可证绑定到设备域。 多个设备可以加入域并接收域令牌。 在域中的设备获得许可证之后，许可证可以传送到域中的任何其他设备，并且这些设备可以播放内容而不需要直接从许可证服务器获得许可证。

要支持绑定域的许可证，策略必须指定客户端必须向其注册的域服务器。 该策略还将指定域服务器的身份验证要求（是否允许匿名访问，或者服务器是否需要用户名/密码或自定义身份验证）。

Adobe访问客户端版本3.0及更高版本支持域注册和域绑定许可证。 如果Flash Player中的较旧客户端或AdobeAccess 3.0客户端请求支持域注册的内容许可证，则许可证服务器可以使用支持绑定到特定设备的替代策略来颁发许可证。
