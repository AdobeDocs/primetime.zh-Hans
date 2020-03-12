---
seo-title: 处理Adobe Primetime DRM请求
title: 处理Adobe Primetime DRM请求
uuid: ee10504d-84f0-472a-b58a-2a87fdeedfc1
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# 处理Adobe Primetime DRM请求 {#process-adobe-primetime-drm-requests}

管理请求的一般方法是创建一个处理函数、解析请求、设置响应数据或错误代码并关闭该处理函数。

用于处理单个请求／响应交互的基类是 `com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`。 类的一个实 `HandlerConfiguration` 例用于初始化该处理函数。 `HandlerConfiguration` 存储服务器配置信息，包括传输凭证、时间戳容差、策略更新列表和撤销列表。处理函数读取请求数据并将请求解析为实例 `RequestMessageBase`。 调用者可以检查请求中的信息并决定是返回错误还是成功响应(子类提 `RequestMessageBase` 供设置响应数据的方法)。

如果请求成功，请设置响应数据；否则，失败 `RequestMessageBase.setErrorData()` 时调用。 始终通过调用方法来 `close()` 结束实现(建议在语 `close()` 句的块 `finally` 中调用 `try` 该方法)。 有关如何调 `MessageHandlerBase` 用处理函数的示例，请参阅API参考文档。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>应发送HTTP状态代码200(OK)以响应处理程序处理的所有请求。 如果由于服务器错误而无法创建该处理函数，则服务器可能会使用其他状态代码做出响应，如500（内部服务器错误）。

客户端使用打包时指定的许可证服务器URL作为发送到许可证服务器的所有请求的基本URL。 例如，如果服务器URL指定为&lt;[!DNL ht<span></span>tps://licenseserver.com/path]>，则客户端会向&lt;[!DNL ht<span></span>tps://licenseserver.com/path/flashaccess/...]>发送请求，有关每种类型的请求所使用的特定路径的详细信息，请参阅以下几节。 实施许可证服务器时，请确保服务器响应每种类型的请求所需的路径。

许可证请求可以包含身份验证令牌。 如果使用用户名／密码身份验证，则请求可能包含由 `AuthenticationToken` 生成的代码 `AuthenticationHandler`，而SDK将确保令牌在发出许可证之前有效。

## 使用机器标识符 {#use-machine-identifiers}

所有Adobe Primetime DRM请求（支持FMRMS兼容性的请求除外）都包括关于在个性化过程中已发送给客户端的机器令牌的信息。 机器令牌包括机器ID，该ID是在个性化期间分配的标识符。 您可以使用此标识符计算用户从中请求许可证或加入域的计算机数。

您可以按如下方式使用标识符：

* 该方 `getUniqueId()` 法返回在个性化期间已分配给设备的字符串。 可以将字符串存储在数据库中并按标识符进行搜索。 但是，如果用户重新设置硬盘的格式并再次个性化，则此标识符会更改。 此标识符在同一台计算机上的不同浏览器中的Adobe AIR和Adobe Flash Player之间也具有不同的值。
* 如果要更准确地计算计算机，可以使用 `getBytes()` 存储整个标识符。 要确定计算机之前是否已被看到，请获取用户名的所有标识符并调用以 `matches()` 检查是否匹配。 由于 `matches()` 要比较返回的值必须使用该方法 `MachineId.getBytes`，因此只有在少量值进行比较时，此选项才可用；例如，与特定用户关联的计算机。

## 用户身份验证 {#user-authentication}

Adobe Primetime DRM请求可包含身份验证令牌。

如果使用用户名／密码身份验证，则请求可能包含由 `AuthenticationToken` 生成的 `AuthenticationHandler`。 如果要访问并验证令牌，您需要使用 `RequestMessageBase.getAuthenticationToken()`。 要在客户端上发起用户名／密码请求，请使 `DRMManager.authenticate()` 用ActionScript或iOS API。

如果客户端和服务器使用自定义身份验证机制，则客户端通过某些其他通道获得身份验证令牌，并使用 `DRMManager.setAuthenticationToken` ActionScript 3.0 API设置自定义身份验证令牌。 使用 `RequestMessageBase.getRawAuthenticationToken()` 获取自定义身份验证令牌。 服务器实现确定自定义身份验证令牌是否有效。

## 重放保护 {#replay-protection}

对于重放保护，您可能希望检查最近是否通过调用看到消息标识符 `RequestMessageBase.getMessageId()`。 如果是，则攻击者可能尝试重播请求，该请求应被拒绝。 为了检测重放尝试，服务器可以存储最近看到的消息ID的列表并针对缓存的列表检查每个传入的请求。 要限制消息标识符需要存储的时间，请调用 `HandlerConfiguration.setTimestampTolerance()`。 如果设置了此属性，则SDK会拒绝任何包含时间戳超过服务器时间指定秒数的请求。

## 回滚检测 {#rollback-detection}

对于回滚检测，某些使用规则要求客户端维护状态信息以执行权限。 例如，为了实施播放窗口使用规则，客户端存储用户首次开始查看内容的日期和时间。 此事件会触发播放窗口的开始。 为了安全地强制播放窗口，服务器需要确保用户不备份和恢复客户端状态，以删除存储在客户端上的播放窗口开始时间。 服务器通过跟踪客户端的回滚计数器的值来执行此操作。

对于每个请求，服务器通过调用获取对象来获取计数器的值， `RequestMessageBase.getClientState()` 然后调 `ClientState` 用 `ClientState.getCounter()` 来获取客户端状态计数器的当前值。 服务器应为每个客户端存储此值(用于标识与回滚计数器值关联的客户端 `MachineId.getUniqueId()` )，然后调用该值 `ClientState.incrementCounter()` 将计数器值增加1。 如果服务器检测到计数器值小于服务器看到的最后一个值，则客户端状态可能已回滚。

有关客户端 `ClientState` 状态篡改检测的更多信息，请参阅API参考文档。

## 全局服务器配置数据{#global-server-configuration-data}

除了许可证服务器使用的配置之外，还存 `HandlerConfiguration` 储可发送到客户端以控制如何实施许可证的配置信息。 这是通过创建类和调 `ServerConfigData` 用完成的 `HandlerConfiguration.setServerConfigData()`。 这些设置仅适用于由此许可证服务器颁发的许可证。

时钟回退容差是许可证服务器可以设置的一个属性，用于控制客户端执行许可证的方式。 默认情况下，用户可以在不使许可证失效的情况下将计算机时钟回退4小时。 如果许可证服务器操作员希望使用其他设置，则可以在类中设置新 `ServerConfigData` 值。 当您更改其中任何设置的值时，请务必通过调用来增加版本号 `setVersion()`。 只有当客户端上的版本比当前版本旧时，新值才会发送到客 `ServerConfigData` 户端。

## 跨域DRM策略文件 {#crossdomain-drm-policy-file}

如果许可证服务器托管在不同于视频播放SWF的域上，则需要跨域DRM策略文件( [!DNL crossdomain.xml])来使SWF能够从许可证服务器请求许可证。 跨域DRM策略文件由XML文件表示，该XML文件使服务器能够指示其数据和文档可用于从其他域提供的SWF文件。 允许从许可证服务器的跨域DRM策略文件中指定的域提供的任何SWF文件访问该许可证服务器的数据或资源。

Adobe建议开发人员在部署跨域策略文件时遵循最佳实践，方法是仅允许受信任的域访问许可证服务器并限制对Web服务器上的许可证子目录的访问。

有关跨域DRM策略文件的详细信息，请参阅以下位置：

* 网站控制（DRM策略文件）
* 跨域DRM策略文件规范： [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)