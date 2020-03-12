---
seo-title: 概述
title: 概述
uuid: 870c32f5-1119-4fec-abed-25e51dd1ebe3
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 概述{#overview}

处理请求的一般方法是创建一个处理函数、解析该请求、设置响应数据或错误代码并关闭该处理函数。

用于处理单个请求／响应交互的基类是 `com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`。 类的一个实 `HandlerConfiguration` 例用于初始化该处理函数。 `HandlerConfiguration` 存储服务器配置信息，包括传输凭证、时间戳容差、策略更新列表和撤销列表。处理函数读取请求数据并将请求解析为实例 `RequestMessageBase`。 调用者可以检查请求中的信息并决定是返回错误还是成功响应(子类提 `RequestMessageBase` 供设置响应数据的方法)。

如果请求成功，请设置响应数据；否则，失败 `RequestMessageBase.setErrorData()` 时调用。 始终通过调用方法来 `close()` 结束实现(建议在语 `close()` 句的块 `finally` 中调用 `try` 该方法)。 有关如何调 `MessageHandlerBase` 用处理函数的示例，请参阅API参考文档。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>应发送HTTP状态代码200(OK)以响应处理程序处理的所有请求。 如果由于服务器错误而无法创建该处理函数，则服务器可能会使用其他状态代码做出响应，如500（内部服务器错误）。

客户端使用打包时指定的许可证服务器URL作为发送到许可证服务器的所有请求的基本URL。 例如，如果服务器URL被指定为“<span></span>https://licenseserver.com/path”，则客户端将向“<span></span>https://licenseserver.com/path/flashaccess/...”发送请求。 有关每种类型的请求所使用的特定路径的详细信息，请参阅以下几节。 实施许可证服务器时，请确保服务器响应每种类型的请求所需的路径。

许可证请求可以包含身份验证令牌。 如果使用用户名／密码身份验证，则请求可能包含由 `AuthenticationToken` 生成的代码 `AuthenticationHandler`，而SDK将确保令牌在发出许可证之前有效。
