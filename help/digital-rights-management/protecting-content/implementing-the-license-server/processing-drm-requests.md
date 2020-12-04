---
seo-title: 处理Adobe PrimetimeDRM请求
title: 处理Adobe PrimetimeDRM请求
uuid: ee10504d-84f0-472a-b58a-2a87fdeedfc1
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '1251'
ht-degree: 0%

---


# 处理Adobe PrimetimeDRM请求{#process-adobe-primetime-drm-requests}

管理请求的一般方法是创建一个处理函数、解析请求、设置响应数据或错误代码并关闭该处理函数。

用于处理单个请求／响应交互的基类为`com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`。 `HandlerConfiguration`类的实例用于初始化处理函数。 `HandlerConfiguration` 存储服务器配置信息，包括传输凭据、时间戳容限、策略更新列表和撤销列表。处理程序读取请求数据并将请求解析为实例 `RequestMessageBase`。调用者可以检查请求中的信息，并决定是返回错误还是成功响应（`RequestMessageBase`的子类提供一种设置响应数据的方法）。

如果请求成功，请设置响应数据；否则，在失败时调用`RequestMessageBase.setErrorData()`。 始终通过调用`close()`方法来结束实现（建议在`try`语句的`finally`块中调用`close()`）。 有关如何调用处理函数的示例，请参阅`MessageHandlerBase` API参考文档。

>[!NOTE]
>
>应发送HTTP状态代码200(OK)以响应处理程序处理的所有请求。 如果由于服务器错误而无法创建该处理程序，则服务器可能会使用其他状态代码做出响应，如500（内部服务器错误）。

客户端使用打包时指定的许可证服务器URL作为发送到许可证服务器的所有请求的基本URL。 例如，如果服务器URL指定为[!DNL ht<span></span>tps://licenseserver.com/path]，则客户端会向&lt;[!DNL ht<span></span>tps://licenseserver.com/path/flashaccess/发送请求……]>有关每种类型的请求所使用的特定路径的详细信息，请参阅以下各节。 实施许可证服务器时，请确保服务器响应每种类型的请求所需的路径。

许可证请求可包含身份验证令牌。 如果使用用户名／密码身份验证，则请求可能包含由`AuthenticationHandler`生成的`AuthenticationToken`,SDK将确保令牌在颁发许可证之前有效。

## 使用计算机标识符{#use-machine-identifiers}

所有Adobe PrimetimeDRM请求（支持FMRMS兼容性的请求除外）都包括关于在个性化期间已发送给客户端的机器令牌的信息。 计算机令牌包括计算机ID，该ID是在个性化过程中分配的标识符。 您可以使用此标识符计算用户请求许可证或加入域的计算机数。

您可以按如下方式使用标识符：

* `getUniqueId()`方法返回在个性化过程中已分配给设备的字符串。 可以将字符串存储在数据库中并按标识符进行搜索。 但是，如果用户重新格式化硬盘并再次个性化，则此标识符会更改。 此标识符在同一台计算机上的不同浏览器中的Adobe AIRFlash Player和Adobe之间也具有不同的值。
* 如果要更准确地计算计算机，可使用`getBytes()`存储整个标识符。 要确定以前是否看到过该计算机，请获取用户名的所有标识符并调用`matches()`检查是否有匹配项。 由于`matches()`方法必须用于比较`MachineId.getBytes`返回的值，因此只有在要比较的值较少时，此选项才实用；例如，与特定用户关联的计算机。

## 用户身份验证{#user-authentication}

Adobe PrimetimeDRM请求可以包含身份验证令牌。

如果使用用户名／密码身份验证，则请求可能包含由`AuthenticationHandler`生成的`AuthenticationToken`。 如果要访问并验证令牌，则需要使用`RequestMessageBase.getAuthenticationToken()`。 要在客户端上启动用户名／密码请求，请使用`DRMManager.authenticate()`ActionScript或iOS API。

如果客户端和服务器使用自定义身份验证机制，则客户端通过某些其他渠道获取身份验证令牌，并使用`DRMManager.setAuthenticationToken`ActionScript3.0 API设置自定义身份验证令牌。 使用`RequestMessageBase.getRawAuthenticationToken()`获取自定义身份验证令牌。 服务器实现确定自定义身份验证令牌是否有效。

## 重放保护{#replay-protection}

对于重放保护，您可能希望通过调用`RequestMessageBase.getMessageId()`检查最近是否看到消息标识符。 如果是，则攻击者可能正在尝试重播请求，应拒绝该请求。 为了检测重放尝试，服务器可以存储最近看到的消息id的列表，并根据缓存的列表检查每个传入请求。 要限制消息标识符需要存储的时间，请调用`HandlerConfiguration.setTimestampTolerance()`。 如果设置了此属性，SDK会拒绝任何包含时间戳超过服务器时间指定秒数的请求。

## 回滚检测{#rollback-detection}

对于回滚检测，某些使用规则要求客户端维护状态信息以执行权限。 例如，要强制执行播放窗口使用规则，客户端存储用户首次开始查看内容的日期和时间。 此事件触发播放窗口的开始。 为了安全地强制播放窗口，服务器需要确保用户不备份和恢复客户端状态，以删除存储在客户端上的播放窗口开始时间。 服务器通过跟踪客户端的回滚计数器的值来执行此操作。

对于每个请求，服务器通过调用`RequestMessageBase.getClientState()`获取`ClientState`对象，然后调用`ClientState.getCounter()`获取客户端状态计数器的当前值来获取计数器的值。 服务器应为每个客户端存储此值（使用`MachineId.getUniqueId()`来标识与回滚计数器值关联的客户端），然后调用`ClientState.incrementCounter()`将计数器值增加1。 如果服务器检测到计数器值小于服务器看到的最后一个值，则客户端状态可能已回滚。

有关客户端状态篡改检测的详细信息，请参阅`ClientState` API参考文档。

## 全局服务器配置数据{#global-server-configuration-data}

除了许可证服务器使用的配置外，`HandlerConfiguration`还存储可发送到客户端以控制如何实施许可证的配置信息。 创建`ServerConfigData`类并调用`HandlerConfiguration.setServerConfigData()`即可完成此操作。 这些设置仅适用于此许可证服务器颁发的许可证。

时钟回退容限是许可证服务器可以设置的一个属性，用于控制客户端执行许可证的方式。 默认情况下，用户可以在不使许可证失效的情况下将计算机时钟设置回4小时。 如果许可证服务器操作员希望使用其他设置，可以在`ServerConfigData`类中设置新值。 当您更改任何这些设置的值时，请务必通过调用`setVersion()`来增加版本号。 只有当客户端上的版本早于当前的`ServerConfigData`版本时，新值才会发送到客户端。

## 跨域DRM策略文件{#crossdomain-drm-policy-file}

如果许可证服务器托管在与视频播放SWF不同的域中，则需要跨域DRM策略文件([!DNL crossdomain.xml])，以使SWF能够从许可证服务器请求许可证。 跨域DRM策略文件由XML文件表示，该XML文件使服务器能够指示其数据和文档可用于从其他域提供的SWF文件。 允许从许可证服务器的跨域DRM策略文件中指定的域提供的任何SWF文件访问该许可证服务器的数据或资源。

Adobe建议开发人员在部署跨域策略文件时遵循最佳实践，方法是仅允许受信任的域访问许可证服务器并限制对Web服务器上许可证子目录的访问。

有关跨域DRM策略文件的详细信息，请参阅以下位置：

* 网站控制（DRM策略文件）
* 跨域DRM策略文件规范：[https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)