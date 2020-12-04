---
seo-title: 概述
title: 概述
uuid: 870c32f5-1119-4fec-abed-25e51dd1ebe3
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---


# 概述{#overview}

处理请求的一般方法是创建一个处理函数、解析该请求、设置响应数据或错误代码并关闭该处理函数。

用于处理单个请求／响应交互的基类为`com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`。 `HandlerConfiguration`类的实例用于初始化处理函数。 `HandlerConfiguration` 存储服务器配置信息，包括传输凭据、时间戳容限、策略更新列表和撤销列表。处理程序读取请求数据并将请求解析为实例 `RequestMessageBase`。调用者可以检查请求中的信息，并决定是返回错误还是成功响应（`RequestMessageBase`的子类提供一种设置响应数据的方法）。

如果请求成功，请设置响应数据；否则，在失败时调用`RequestMessageBase.setErrorData()`。 始终通过调用`close()`方法来结束实现（建议在`try`语句的`finally`块中调用`close()`）。 有关如何调用处理函数的示例，请参阅`MessageHandlerBase` API参考文档。

>[!NOTE]
>
>应发送HTTP状态代码200(OK)以响应处理程序处理的所有请求。 如果由于服务器错误而无法创建该处理程序，则服务器可能会使用其他状态代码做出响应，如500（内部服务器错误）。

客户端使用打包时指定的许可证服务器URL作为发送到许可证服务器的所有请求的基本URL。 例如，如果服务器URL指定为“ht<span></span>tps://licenseserver.com/path”，则客户端将向“ht<span></span>tps://licenseserver.com/path/flashaccess/...”发送请求。 有关每种类型请求所使用的特定路径的详细信息，请参阅以下各节。 实施许可证服务器时，请确保服务器响应每种类型的请求所需的路径。

许可证请求可包含身份验证令牌。 如果使用用户名／密码身份验证，则请求可能包含由`AuthenticationHandler`生成的`AuthenticationToken`,SDK将确保令牌在颁发许可证之前有效。
