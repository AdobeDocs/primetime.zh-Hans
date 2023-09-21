---
title: 处理Adobe Primetime DRM请求
description: 处理Adobe Primetime DRM请求
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1251'
ht-degree: 0%

---

# 处理Adobe Primetime DRM请求 {#process-adobe-primetime-drm-requests}

管理请求的一般方法是创建处理程序、解析请求、设置响应数据或错误代码并关闭处理程序。

用于处理单个请求/响应交互的基类是 `com.adobe.flashaccess.sdk.protocol.MessageHandlerBase`. 的实例 `HandlerConfiguration` 类用于初始化处理程序。 `HandlerConfiguration` 存储服务器配置信息，包括传输凭据、时间戳容错、策略更新列表和吊销列表。处理程序读取请求数据并将请求解析为的实例 `RequestMessageBase`. 调用方可以检查请求中的信息，并决定返回错误还是成功响应（的子类） `RequestMessageBase` 提供了一种设置响应数据的方法)。

如果请求成功，则设置响应数据；否则，调用 `RequestMessageBase.setErrorData()` 失败时。 始终通过调用 `close()` 方法(建议 `close()` 在中调用 `finally` 块 `try` 语句)。 请参阅 `MessageHandlerBase` 有关如何调用处理程序的示例的API参考文档。

>[!NOTE]
>
>应发送HTTP状态代码200 (OK)以响应处理程序处理的所有请求。 如果由于服务器错误而无法创建处理程序，则服务器可能会以其他状态代码响应，如500（内部服务器错误）。

客户端使用打包时指定的许可证服务器URL作为发送到许可证服务器的所有请求的基本URL。 例如，如果将服务器URL指定为&lt;[!DNL ht<span></span>tps://licenseserver.com/path]>，客户端随后将请求发送给&lt;[!DNL ht<span></span>tps://licenseserver.com/path/flashaccess/...]>有关用于每种类型请求的特定路径的详细信息，请参阅以下部分。 实施许可证服务器时，请确保服务器响应每种类型请求所需的路径。

许可证请求可以包含身份验证令牌。 如果使用用户名/密码身份验证，请求可能包含 `AuthenticationToken` 生成者 `AuthenticationHandler`，并且SDK将在颁发许可证之前确保令牌有效。

## 使用计算机标识符 {#use-machine-identifiers}

所有Adobe Primetime DRM请求（支持FMRMS兼容性的请求除外）都包含有关在个性化期间颁发给客户端的计算机令牌的信息。 计算机令牌包括计算机ID，它是已在个性化期间分配的标识符。 您可以使用此标识符计算用户从中请求许可证或加入域的计算机数量。

您可以使用标识符，如下所示：

* 此 `getUniqueId()` 方法会返回在个性化期间分配给设备的字符串。 您可以将字符串存储在数据库中，并按标识符进行搜索。 但是，如果用户重新格式化硬盘驱动器并再次对其进行个性化，则此标识符会发生变化。 同一台计算机上不同浏览器中的Adobe AIR和AdobeFlash Player之间，此标识符的值也不同。
* 如果要更准确地计算计算机数，可以使用 `getBytes()` 用于存储整个标识符。 要确定以前是否看到过该计算机，请获取用户名的所有标识符并调用 `matches()` 以检查是否匹配。 因为 `matches()` 方法必须用于比较返回的值 `MachineId.getBytes`，此选项仅当要比较的值数量较少时（例如，与特定用户关联的计算机）才具有实用性。

## 用户身份验证 {#user-authentication}

Adobe Primetime DRM请求可以包含身份验证令牌。

如果使用用户名/密码身份验证，请求可能包括 `AuthenticationToken` 生成者 `AuthenticationHandler`. 如果要访问并验证令牌，则需要使用 `RequestMessageBase.getAuthenticationToken()`. 要在客户端上启动用户名/密码请求，请使用 `DRMManager.authenticate()` ActionScript或iOS API。

如果客户端和服务器使用自定义身份验证机制，则客户端通过其他渠道获取身份验证令牌，并使用设置自定义身份验证令牌 `DRMManager.setAuthenticationToken` ActionScript3.0 API。 使用 `RequestMessageBase.getRawAuthenticationToken()` 以获取自定义身份验证令牌。 服务器实施将确定自定义身份验证令牌是否有效。

## 重播保护 {#replay-protection}

对于重放保护，您可能希望通过调用检查最近是否看到消息标识符 `RequestMessageBase.getMessageId()`. 如果是这样，攻击者可能会尝试重放该请求，但应拒绝该请求。 为了检测重放尝试，服务器可以存储最近查看过的消息ID列表，并根据缓存的列表检查每个传入请求。 要限制需要存储消息标识符的时间，请调用 `HandlerConfiguration.setTimestampTolerance()`. 如果设置了此属性，则SDK随后会拒绝任何携带时间戳超过服务器时间指定秒数的请求。

## 回滚检测 {#rollback-detection}

对于回滚检测，某些使用规则要求客户端维护用于实施权限的状态信息。 例如，要强制实施播放窗口使用规则，客户端将存储用户首次开始查看内容的日期和时间。 此事件会触发播放窗口的启动。 要安全地强制执行播放窗口，服务器需要确保用户没有备份和还原客户端状态，以删除存储在客户端上的播放窗口开始时间。 服务器通过跟踪客户端回滚计数器的值来执行此操作。

对于每个请求，服务器通过调用获取计数器的值 `RequestMessageBase.getClientState()` 以获取 `ClientState` 对象，然后调用 `ClientState.getCounter()` 以获取客户端状态计数器的当前值。 服务器应该为每个客户端存储此值(使用 `MachineId.getUniqueId()` 标识与回退计数器值关联的客户端)，然后调用 `ClientState.incrementCounter()` 将计数器值增加1。 如果服务器检测到计数器值小于服务器看到的最后一个值，则客户端状态可能已回滚。

请参阅 `ClientState` API参考文档，了解有关客户端状态篡改检测的更多信息。

## 全局服务器配置数据{#global-server-configuration-data}

除了许可证服务器使用的配置外， `HandlerConfiguration` 存储可以发送到客户端的配置信息，以控制许可证的实施方式。 这是通过创建 `ServerConfigData` 类和调用 `HandlerConfiguration.setServerConfigData()`. 这些设置仅适用于此许可证服务器颁发的许可证。

时钟回溯容限是许可证服务器可以设置的一个属性，用于控制客户端强制执行许可证的方式。 默认情况下，用户可以在不使许可证失效的情况下将其计算机时钟向后设置4小时。 如果许可证服务器操作员希望使用不同的设置，则可以在以下位置设置新值： `ServerConfigData` 类。 在更改其中任何设置的值时，请确保通过调用递增版本号 `setVersion()`. 仅当客户端上的版本比当前版本旧时，才会将新值发送到客户端 `ServerConfigData` 版本。

## 跨域DRM策略文件 {#crossdomain-drm-policy-file}

如果许可证服务器托管在不同于视频播放SWF的域上，则使用跨域DRM策略文件( [!DNL crossdomain.xml])以使SWF能够向许可证服务器请求许可证。 跨域DRM策略文件由XML文件表示，该文件使服务器能够指示其数据和文档可用于SWF从其他域提供的文件。 从许可证服务器的跨域DRM策略文件中指定的域提供的任何SWF文件都允许从该许可证服务器访问数据或资产。

Adobe建议开发人员在部署跨域策略文件时遵循最佳实践，仅允许受信任域访问许可证服务器，并限制对Web服务器上许可证子目录的访问。

有关跨域DRM策略文件的详细信息，请参阅以下位置：

* 网站控件（DRM策略文件）
* 跨域DRM策略文件规范： [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)
