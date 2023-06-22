---
title: 概述
description: 概述
copied-description: true
exl-id: d284b279-d261-4573-825d-919a551b3194
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# 概述{#overview}

处理请求的一般方法是创建处理程序、解析请求、设置响应数据或错误代码，以及关闭处理程序。

用于处理单个请求/响应交互的基类是 `com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`. 的实例 `HandlerConfiguration` 类用于初始化处理程序。 `HandlerConfiguration` 存储服务器配置信息，包括传输凭据、时间戳公差、策略更新列表和吊销列表。处理程序读取请求数据并将请求解析为的实例 `RequestMessageBase`. 调用方可以检查请求中的信息，并决定是返回错误还是成功响应（的子类） `RequestMessageBase` 提供了一种设置响应数据的方法)。

如果请求成功，则设置响应数据；否则，调用 `RequestMessageBase.setErrorData()` 失败时。 始终通过调用 `close()` 方法(建议您 `close()` 在中调用 `finally` 块 `try` 语句)。 请参阅 `MessageHandlerBase` 有关如何调用处理程序的示例的API参考文档。

>[!NOTE]
>
>应发送HTTP状态代码200 (OK)以响应处理程序处理的所有请求。 如果由于服务器错误而无法创建处理程序，则服务器可能会以其他状态代码响应，例如500（内部服务器错误）。

客户端使用打包时指定的许可证服务器URL作为发送到许可证服务器的所有请求的基本URL。 例如，如果将服务器URL指定为“ht”<span></span>tps://licenseserver.com/path”时，客户端将向“ht”发送请求<span></span>tps://licenseserver.com/path/flashaccess/...”。 有关用于每种类型请求的特定路径的详细信息，请参阅以下部分。 实施许可证服务器时，请确保服务器响应每种类型请求所需的路径。

许可证请求可以包含身份验证令牌。 如果使用用户名/密码身份验证，请求可能包含 `AuthenticationToken` 生成者 `AuthenticationHandler`，并且SDK将确保令牌在颁发许可证之前有效。
