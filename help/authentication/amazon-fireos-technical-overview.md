---
title: Amazon FireOS技术概述
description: Amazon FireOS技术概述
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2142'
ht-degree: 0%

---


# Amazon FireOS技术概述 {#amazon-fireos-technical-overview}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

</br>

## 简介 {#intro}

Amazon FireOS AccessEnabler由两个组件表示：应用程序使用的AccessEnabler存根库和系统级Java Android库，使移动应用程序能够对TV Everywhere的授权服务使用Adobe Primetime身份验证。 Amazon FireOS的Android实施包括定义授权API的AccessEnabler接口和描述库触发的回调的EntitlementDelegate协议。 系统级别的AccessEnabler Android库允许访问Amazon服务，以便在平台级别启用单点登录。

## 了解本机客户端工作流 {#native_client_workflows}

本机客户端工作流通常与基于浏览器的Primetime身份验证客户端的工作流相同或非常相似。 但是，也有一些例外，如下所述。


### 初始化后工作流 {#post-init}

AccessEnabler支持的所有授权工作流都假定您之前调用了 [`setRequestor()`](#setRequestor) 建立你的身份。 此调用仅提供一次请求者ID，通常是在应用程序的初始化/设置阶段进行。

在初次调用 [`setRequestor()`](#setRequestor)，则可以选择如何继续：

- 您可以立即开始发起授权调用，并根据需要允许它们静默排入队列。
- 或者，您也可以收到 [`setRequestor()`](#setRequestor) 通过实现setRequestorComplete()回调。
- 或者，两者兼得。

至于是否等待通知是否成功，取决于您 [`setRequestor()`](#setRequestor) 或依赖AccessEnabler的呼叫队列机制。 由于所有后续的授权和身份验证请求都需要请求者ID和关联的配置信息，因此 [`setRequestor()`](#setRequestor) 方法会在初始化完成之前有效阻止所有身份验证和授权API调用。

### 一般初始身份验证工作流 {#generic}

此工作流的目的是使用用户的MVPD登录用户。  成功登录后，后端服务器会向用户发出身份验证令牌。 虽然身份验证通常作为授权过程的一部分完成，但下面描述了身份验证如何单独工作，并且不包括任何授权步骤。

请注意，虽然以下本机客户端工作流与典型的基于浏览器的身份验证工作流不同，但是对于本机客户端和基于浏览器的客户端，步骤1-5是相同的：

1. 您的页面或播放器通过调用 [getAuthentication()](#getAuthN)，用于检查有效的缓存身份验证令牌。 此方法具有可选 `redirectURL` 参数；如果不为 `redirectURL`，成功验证后，会将用户返回到初始化身份验证的URL。
1. AccessEnabler确定当前身份验证状态。 如果用户当前已通过身份验证，则AccessEnabler会调用 `setAuthenticationStatus()` 回调函数，传递指示成功的身份验证状态（下面的步骤7）。
1. 如果用户未进行身份验证，AccessEnabler将继续验证流程，方法是确定用户上次的验证尝试是否与给定MVPD成功。 如果MVPD ID已缓存，并且 `canAuthenticate` 标记为true，或者使用 [`setSelectedProvider()`](#setSelectedProvider)，则系统不会在MVPD选择对话框中提示用户。 验证流程会继续使用MVPD的缓存值（即，上次成功验证期间使用的相同MVPD）。 系统会向后端服务器发起网络调用，并将用户重定向到MVPD登录页面（下面的步骤6）。
1. 如果没有缓存MVPD ID，并且未使用 [`setSelectedProvider()`](#setSelectedProvider) 或 `canAuthenticate` 标记设置为false， [`displayProviderDialog()`](#displayProviderDialog) 调用回调。 此回调将指导您的页面或播放器创建UI，以向用户显示可供选择的MVPD列表。 提供了MVPD对象数组，其中包含构建MVPD选择器所需的信息。 每个MVPD对象都描述一个MVPD实体，并包含MVPD的ID（例如XFINITY、AT\&amp;T等）等信息 和可找到MVPD徽标的URL。
1. 选择特定MVPD后，您的页面或播放器必须将用户选择的通知AccessEnabler。 对于非Flash客户端，一旦用户选择所需的MVPD，您将通过对 [`setSelectedProvider()`](#setSelectedProvider) 方法。 Flash客户端而是派送共享 `MVPDEvent` 类型“`mvpdSelection`“ ”，传递选定的提供程序。
1. 对于Amazon应用程序， [`navigateToUrl()`](#navigagteToUrl) 将忽略回调。 Access Enabler库有助于访问通用的WebView控件来验证用户。
1. 通过 `WebView`，则用户将访问MVPD的登录页面并输入其凭据。 请注意，在此传输过程中会发生多个重定向操作。 
1. WebView完成身份验证后，将关闭并通知AccessEnabler用户已成功登录， AccessEnabler将从后端服务器中检索实际的身份验证令牌。 AccessEnabler将调用 [`setAuthenticationStatus()`](#setAuthNStatus) 状态代码为1的回调，表示成功。 如果在执行这些步骤期间出错，则 [`setAuthenticationStatus()`](#setAuthNStatus) 回调会使用状态代码为0触发，并且还会触发相应的错误代码，以指示用户未进行身份验证。

### 注销工作流 {#logout}

对于本机客户端，注销的处理方式与上述身份验证过程类似。 按照此模式， AccessEnabler将创建 `WebView` 控件和将在后端服务器上使用注销端点的URL加载控件。 注销过程完成后，将清除令牌。

请注意，注销流程与验证流程不同，因为用户无需与 `WebView` 无论如何。 注销完成后， AccessEnabler将调用 `setAuthenticationStatus()` 状态代码为0的回调，表示用户未进行身份验证。

## 令牌 {#tokens}

### 定义和使用 {#definitions}

Primetime身份验证授权解决方案围绕生成特定数据（令牌），在身份验证和授权工作流成功完成后，Primetime身份验证会生成这些数据（令牌）。 这些令牌存储在客户端的Amazon FireOS设备上的本地。

令牌的有效期有限；到期后，需要通过重新启动身份验证和/或授权工作流来重新发布令牌。

授权工作流期间颁发的令牌有三种类型：

- **身份验证令牌**  — 用户身份验证工作流的最终结果将是身份验证GUID，AccessEnabler可以使用它代表用户进行授权查询。 此身份验证GUID将具有关联的生存时间(TTL)值，该值可能与用户的身份验证会话本身不同。 Primetime身份验证通过将身份验证GUID绑定到启动身份验证请求的设备来生成身份验证令牌。
- **授权令牌**  — 授予对由唯一 `resourceID`. 它包括授权方签发的授权补助金和原件 `resourceID`. 此信息绑定到启动请求的设备。
- **短暂的媒体令牌** - AccessEnabler通过返回短时间的媒体令牌，授予对给定资源的托管应用程序的访问权限。 此令牌基于之前为该特定资源获取的授权令牌生成。 此外，此令牌未绑定到设备，并且关联的生命周期会显着缩短(默认：5分钟)。

成功进行身份验证和授权后，Primetime身份验证将发出身份验证、授权和短期媒体令牌。 这些令牌应缓存在用户设备上，并在其关联生命周期内使用。

### 缓存准则 {#caching}


#### 身份验证令牌

- **适用于FireOS 1.10.1的AccessEnabler **基于适用于Android 1.9.1的AccessEnabler — 此SDK引入了一种新的令牌存储方法，可启用多个程序员 — MVPD存储段，从而允许多个身份验证令牌。 

#### 授权令牌

在任何给定时刻，AccessEnabler都只会缓存每个资源的一个授权令牌。 可以缓存多个授权令牌，但它们与不同资源关联。 每当发出新授权令牌且同一资源已存在旧令牌时，新令牌都会覆盖现有的缓存值。

#### 媒体令牌 

根本不应缓存短期媒体令牌。 每次调用授权API时，应从服务器中检索媒体令牌，因为该令牌仅限一次性使用。

### 持久性 {#persistence}

令牌需要在同一应用程序的连续运行中持续保留。 这意味着一旦获取了身份验证和授权令牌并且用户关闭了应用程序，则当用户重新打开应用程序时，应用程序将可以使用相同的令牌。 此外，这些令牌在多个应用程序中是持久的。 换言之，当用户使用一个应用程序通过特定身份提供者登录（成功获取身份验证和授权令牌）后，同一令牌可通过其他应用程序使用，并且当通过同一身份提供者登录时，不再提示用户输入凭据。

这种类型的无缝身份验证/授权工作流程使Primetime身份验证解决方案成为真正的TV-Everywhere实施。 从纯粹的工程角度来看，Android AccessEnabler库通过将令牌数据存储到位于外部存储上的数据库文件中来解决跨应用程序数据共享问题。 此系统级别的共享资源提供了关键要素，这些要素支持实施所需的永久令牌用例：

- 支持结构化存储 — Primetime身份验证令牌存储不仅是简单的线性缓冲类内存结构。 它提供了类似词典的存储机制，该机制允许根据用户指定的键值进行数据索引。
- 支持使用基础文件系统的数据持久性 — 默认情况下，数据库文件的内容会持久保留，并且数据会保存在设备的外部内存中。

将特定令牌放入令牌缓存后，AccessEnabler库将在不同时间检查其有效性。  有效的令牌定义为：

- 令牌的TTL未过期
- 令牌的颁发者包含在允许的身份提供程序列表中

令牌存储可支持多个程序员 — MVPD组合，它依赖于能够容纳多个验证令牌的多级嵌套映射结构。 此新存储不会以任何方式影响AccessEnabler公共API，也不需要程序员进行更改。 以下示例说明了此新功能：

1. 打开App1（由Programmer1开发）。
1. 通过MVPD1（与Programmer1集成）进行身份验证。
1. 暂停/关闭当前应用程序，并打开App2（由Programmer2开发）。
1. 假设Programmer2未与MVPD2集成；因此，用户将不会在App2中进行身份验证。
1. 在App2中使用MVPD2（与Programmer2集成）进行身份验证。
1. 切换回App1；用户仍将通过Programmer1的身份验证。

### 格式 {#format}

#### 身份验证令牌 {#authn_token}

下面列出了身份验证令牌的格式：

```JSON
    <signatureInfo>base64(...)<signatureInfo>
    <simpleAuthenticationToken>
        <simpleTokenAuthenticationGuid>71C69B91-F327-F185-F29E-2CE20DC560F5</simpleTokenAuthenticationGuid>
        <simpleTokenRequestorID>TEST_REQUESTOR</simpleTokenRequestorID>
        <simpleTokenDomainName>adobe.com</simpleTokenDomainName>
        <simpleTokenExpires>2011/03/19 02:29:34 GMT +0200</simpleTokenExpires>
        <simpleTokenMsoID>Adobe</simpleTokenMsoID>
        <simpleTokenDeviceID>
            <simpleTokenFingerprint>
                HASH(true device identification info)
            </simpleTokenFingerprint>
        </simpleTokenDeviceID>   
    </simpleAuthenticationToken>
```
 

#### 授权令牌 {#authz_token}

下面列出了授权令牌的格式：

```JSON
    <signatureInfo>base64(...)<signatureInfo>
    <simpleAuthorizationToken>
        <simpleTokenRequestorID>TEST_REQUESTOR</simpleTokenRequestorID>
        <simpleTokenResourceID>TEST_RESOURCE</simpleTokenResourceID>
        <simpleTokenTTL>2011/03/17 14:40:08 GMT +0200</simpleTokenTTL>
        <simpleTokenMsoID>Adobe</simpleTokenMsoID>
        <simpleTokenDeviceID>
            <simpleTokenFingerprint>
                HASH(true device identification info)
            </simpleTokenFingerprint>
        </simpleTokenDeviceID>
    </simpleAuthorizationToken>
```


#### 短媒体令牌 {#short_media_token}

下面列出了短媒体令牌的格式。  此令牌会向程序员的应用程序公开。  在成功的授权流程结束时，它被传递到程序员的应用程序中：

```JSON
    <signatureInfo>signature<signatureInfo>
    <shortAuthorizationToken>
      <sessionGUID>session_guid</sessionGUID>
      <requestorID>requestor_id</requestorID>
      <resourceID>resource_id</resourceID>
      <ttl>ttl_in_ms</ttl>
      <issueTime>issue_time</issueTime>
      <mvpdId>mvpd_id</mvpdId>
      <proxyMvpdId>proxy_mvpd_id</proxyMvpdId>
    </shortAuthorizationToken>
```
 

#### 设备绑定 {#device_binding}

在上面的XML列表中，请注意标有的标记 `simpleTokenFingerprint`. 此标记的用途是保存本机设备ID个性化信息。 AccessEnabler库能够获取此类个性化信息，并在授权调用期间将其提供给Primetime身份验证服务。 该服务将使用此信息并将其嵌入到实际的令牌中，从而有效地将令牌绑定到特定设备。 最终目标是使令牌不能跨设备转让。

在上述XML列表中，请注意标题为simpleTokenFinterprint的标记。 此标记的用途是保存本机设备ID个性化信息。 AccessEnabler库能够获取此类个性化信息，并在授权调用期间将其提供给Primetime身份验证服务。 该服务将使用此信息并将其嵌入到实际的令牌中，从而有效地将令牌绑定到特定设备。 最终目标是使令牌不能跨设备转让。

由于这显然是一项与安全相关的功能，因此从安全角度来看，此信息具有内在的“敏感”性。 因此，需要保护这些信息，使其不受篡改和窃听。 通过通过HTTPS协议发送身份验证/授权请求，可解决窃听问题。 通过对设备标识信息进行数字签名来处理篡改保护。 AccessEnabler库根据设备提供的信息计算设备ID，然后将设备ID“清除”作为请求参数发送到Primetime身份验证服务器。  Primetime身份验证服务器使用Adobe的私钥对设备ID进行数字签名，并将其添加到返回到AccessEnabler的身份验证令牌中。 因此，设备ID与身份验证令牌绑定。  在授权流程中， AccessEnabler会再次以清除方式发送设备ID以及身份验证令牌。  验证过程失败会自动导致验证/授权工作流失败。  Primetime身份验证服务器将私钥应用于设备ID，并将其与身份验证令牌中的值进行比较。  如果二者不匹配，则授权流程将失败。
