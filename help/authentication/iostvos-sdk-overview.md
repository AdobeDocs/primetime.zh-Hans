---
title: iOS/tvOS SDK概述
description: 'iOS/tvOS SDK概述 '
source-git-commit: 6b9508e56bdaa4876bd0974bf7877fb0c1810919
workflow-type: tm+mt
source-wordcount: '3693'
ht-degree: 0%

---


# iOS/tvOS SDK概述 {#iostvos-sdk-overview}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。


</br>


## 简介 {#intro}

iOS AccessEnabler是一个Objective C iOS/tvOS库，它使移动应用程序能够对TV Everywhere的授权服务使用Adobe Primetime身份验证。 实施包括 *AccessEnabler* 定义权利API和 *EntitlementDelegate* 和 *[权利状态](#ios%20entitlement%20status)* 描述库触发的回调的协议。 该接口与协议一起使用一个通用名称：AccessEnabler库。

## iOS和tvOS要求 {#reqs}

有关与iOS和tvOS平台以及Primetime身份验证相关的当前技术要求，请参阅 [平台/设备/工具要求](#ios)，并查阅SDK下载附带的发行说明。 在本页的其余部分中，您将看到一些部分，其中注释了适用于特定SDK版本及更高版本的更改。 例如，以下是关于1.7.5 SDK的合法说明：

## 了解本机客户端工作流 {#flows}

本机客户端工作流通常与基于浏览器的Primetime身份验证客户端的工作流相同或非常相似。 但是，也有一些例外，如下所述。

- [初始化后工作流](#post-init)
- [一般初始身份验证工作流](#generic)
- [注销工作流](#logout)


### 初始化后工作流 {#post-init}

AccessEnabler支持的所有授权工作流都假定您之前调用了 [`setRequestor()`](#setReq) 建立你的身份。 此调用仅提供一次请求者ID，通常是在应用程序的初始化/设置阶段进行。


使用iOS本机客户端，在初次调用 [`setRequestor()`](#setReq)，则可以选择如何继续：

- 您可以立即开始发起授权调用，并根据需要允许它们静默排入队列。

- 您可以收到有关 [`setRequestor()`](#setReq) 执行 [`setRequestorComplete()`](#setReqComplete) 回调。

- 您可以同时执行上述两项操作。

您可以选择让应用程序等待通知 [`setRequestor()`](#setReq) 或者让它依赖AccessEnabler的呼叫队列机制。 由于所有后续的授权和身份验证请求都需要请求者ID和关联的配置信息，因此 [`setRequestor()`](#setReq) 方法会在初始化完成之前有效阻止所有身份验证和授权API调用。

 

### 一般初始身份验证工作流 {#generic}

此工作流的目的是使用用户的MVPD登录用户。 成功登录后，后端服务器会向用户发出身份验证令牌。 虽然身份验证通常作为授权过程的一部分完成，但下面描述了身份验证如何单独工作，并且不包括任何授权步骤。

请注意，虽然本机客户端的此工作流不同于典型的基于浏览器的身份验证工作流，但是对于本机客户端和基于浏览器的客户端，步骤1-5是相同的。

1. 您的应用程序通过调用AccessEnabler的 `getAuthentication() `API方法，用于检查是否有效的缓存身份验证令牌。
1. 如果用户当前已通过身份验证，则AccessEnabler会调用 [`setAuthenticationStatus()`](#setAuthNStatus) 回调函数，传递指示成功的身份验证状态，并结束流程。
1. 如果用户当前未进行身份验证， AccessEnabler将继续身份验证流程，方法是确定用户的上次身份验证尝试是否与给定MVPD成功。 如果MVPD ID已缓存，并且 `canAuthenticate` 标记为true，或者使用 [`setSelectedProvider()`](#setSelProv)，则系统不会在MVPD选择对话框中提示用户。 验证流程会继续使用MVPD的缓存值（即，上次成功验证期间使用的相同MVPD）。 系统会向后端服务器发起网络调用，并将用户重定向到MVPD登录页面（下面的步骤6）。
1. 如果没有缓存MVPD ID，并且未使用 [`setSelectedProvider()`](#setSelProv) 或 `canAuthenticate` 标记设置为false， [`displayProviderDialog()`](#dispProvDialog) 调用回调。 此回调将指示您的应用程序创建UI，以向用户显示要从中选择的MVPD列表。 提供了MVPD对象数组，其中包含构建MVPD选择器所需的信息。 每个MVPD对象都描述一个MVPD实体，并包含MVPD的ID（例如XFINITY、AT\&amp;T等）等信息 和可找到MVPD徽标的URL。
1. 选择特定MVPD后，您的应用程序必须通知AccessEnabler用户选择。 用户选择所需的MVPD后，您将通过对 [`setSelectedProvider()`](#setSelProv) 方法。
1. iOS AccessEnabler将调用 `navigateToUrl:` 回调或 `navigateToUrl:useSVC:` 回调可将用户重定向到MVPD登录页面。 通过触发任一个， AccessEnabler会向您的应用程序请求创建 `UIWebView/WKWebView or SFSafariViewController` 控制器和，以加载回调中提供的URL `url` 参数。 这是后端服务器上身份验证端点的URL。 对于tvOS AccessEnabler， [status()](#status_callback_implementation) 通过 `statusDictionary` 参数和第二个屏幕身份验证的轮询会立即启动。 的 `statusDictionary` 包含 `registration code` 需要用于第二个屏幕身份验证。 
1. 如果是iOS AccessEnabler，则用户将登陆MVPD的登录页面，以通过应用程序的介质输入其凭据 `UIWebView/WKWebView or SFSafariViewController `控制器。 请注意，在此传输过程中会发生多个重定向操作，您的应用程序必须监控控制器在多个重定向操作期间加载的URL。
1. 对于iOS AccessEnabler， `UIWebView/WKWebView or SFSafariViewController` 控制器加载您的应用程序必须关闭控制器并调用AccessEnabler的特定自定义URL `handleExternalURL:url `API方法。 请注意，此特定的自定义URL实际上无效，并且不希望控制器实际加载它。 它只能由您的应用程序解释为验证流程已完成并且关闭安全的信号 `UIWebView/WKWebView or SFSafariViewController` 控制器。 如果您的应用程序需要使用 `SFSafariViewController `控制器特定自定义URL由 `application's custom scheme` (例如： `adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`)，否则，此特定的自定义URL由 `ADOBEPASS_REDIRECT_URL` 常量(即 `adobepass://ios.app`)。
1. 在您的应用程序关闭 `UIWebView/WKWebView or SFSafariViewController` 控制器和调用AccessEnabler的 `handleExternalURL:url `API方法中， AccessEnabler从后端服务器中检索身份验证令牌，并通知您的应用程序身份验证流程已完成。 AccessEnabler将调用 [`setAuthenticationStatus()`](#setAuthNStatus) 状态代码为1的回调，表示成功。 如果在执行这些步骤期间出错，则 [`setAuthenticationStatus()`](#setAuthNStatus) 回调使用状态代码为0触发，表示身份验证失败以及相应的错误代码。


>[!WARNING]
>
> 在AccessEnabler将控制权放弃给您的应用程序的步骤（即，当显示提供商选择对话框，或者当显示UIWebView/WKWebView或SFSafariViewController时）中，用户有机会取消身份验证流程。 在这些情况下，您的应用程序将负责向AccessEnabler通知此事件并调用 [`setSelectedProvider()`](#setSelProv) API方法，将null作为参数传递。 这使AccessEnabler有机会清除其内部状态并重置身份验证流。 在tvOS上，您可以使用相同的方法取消身份验证轮询。


### 注销工作流 {#logout}

对于本机客户端，注销的处理方式与上述身份验证过程类似。

1. 您的应用程序通过调用AccessEnabler启动注销工作流 `logout() `API方法。 注销是一系列HTTP重定向操作的结果，因为用户需要从Primetime身份验证服务器以及MVPD服务器注销。 由于此流程无法通过AccessEnabler库发出的简单HTTP请求来完成，因此， `UIWebView/WKWebView or SFSafariViewController` 控制器需要进行实例化，才能执行HTTP重定向操作。

1. 采用与认证流类似的模式。 iOS AccessEnabler会触发 `navigateToUrl:` 回调或 `navigateToUrl:useSVC:` 创建 `UIWebView/WKWebView or SFSafariViewController` 控制器和，以加载回调中提供的URL `url` 参数。 这是后端服务器上注销端点的URL。 对于tvOS AccessEnabler， `navigateToUrl:` 回调或 `navigateToUrl:useSVC:` 调用回调。

1. 在进行多次重定向时，您的应用程序必须监控 `UIWebView/WKWebView or SFSafariViewController `控制器并检测加载特定自定义URL的时间。 请注意，此特定的自定义URL实际上无效，并且不希望控制器实际加载它。 它只能被您的应用程序解释为注销流程已完成并且关闭控制器是安全的信号。 当控制器加载此特定的自定义URL时，您的应用程序必须关闭控制器并调用AccessEnabler的 `handleExternalURL:url `API方法。 如果您的应用程序需要使用 `SFSafariViewController `控制器特定自定义URL由 `application's custom scheme` (例如，`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`)，否则，此特定的自定义URL由 ` ADOBEPASS_REDIRECT_URL  `常量(即 `adobepass://ios.app`)。

1. 最后， AccessEnabler将调用 [`setAuthenticationStatus()`](#setAuthNStatus) 状态代码为0的回调，表示注销流程成功。

注销流程与验证流程不同，因为用户不需要与 `UIWebView/WKWebView or SFSafariViewController`  控制者。 因此，Adobe建议您在注销过程中使控件不可见（即隐藏）。

## 令牌 {#tokens}

- [定义和使用](#definitions)
- [缓存准则](#caching)
- [持久性](#persistence)
- [格式](#format)
- [设备绑定](#device_binding)


### 定义和使用 {#definitions}

Primetime身份验证授权解决方案围绕生成特定数据（令牌），在身份验证和授权工作流成功完成后，Primetime身份验证会生成这些数据（令牌）。 这些令牌存储在客户端的iOS设备上的本地。

 

令牌的有效期有限；到期后，需要通过重新启动身份验证和/或授权工作流来重新发布令牌。

 

授权工作流期间颁发的令牌有三种类型：

- **身份验证令牌：** 用户身份验证工作流的最终结果将是身份验证GUID，AccessEnabler可以使用它代表用户进行授权查询。 此身份验证GUID将具有关联的生存时间(TTL)值，该值可能与用户的身份验证会话本身不同。 验证令牌将通过将验证GUID绑定到启动验证请求的设备来生成。
- **授权令牌：** 授予对由唯一资源ID标识的特定受保护资源的访问权限。 它包含由授权方签发的授权授权以及原始resourceID。 此信息绑定到启动请求的设备。
- **短暂的媒体令牌：** AccessEnabler通过返回短时间的媒体令牌，授予对给定资源的托管应用程序的访问权限。 此令牌基于之前为该特定资源获取的授权令牌生成。 此外，此令牌未绑定到设备，并且关联的生命周期会显着缩短(默认：5分钟)。

成功进行身份验证和授权后，Primetime身份验证将发出身份验证、授权和短期媒体令牌。 这些令牌应缓存在用户设备上，并在其关联生命周期内使用。

 

### 缓存准则 {#caching}

- 身份验证令牌
- 授权令牌
- 短暂的媒体令牌


#### 身份验证令牌

- **AccessEnabler 1.7:** 此SDK引入了一种新的令牌存储方法，它支持多个程序员 — MVPD存储段，从而支持多个身份验证令牌。 现在，“每个请求者进行身份验证”方案和正常身份验证流程都使用相同的存储布局。 两者唯一的区别在于身份验证的执行方式：“每个请求者的身份验证”包含一项新的改进（被动身份验证），该改进使AccessEnabler能够基于存储中存在的身份验证令牌（对于其他程序员）执行后通道身份验证。 用户只需进行一次身份验证，此会话将用于在其他应用程序中获取身份验证令牌。 此后通道流在 [`setRequestor()`](#setReq) 调用，并且对程序员大多是透明的。 **但是，这里有一个重要要求：程序员必须从主UI线程中调用setRequestor()。**
- **AccessEnabler 1.6及更低版本：** 身份验证令牌在设备上的缓存方式取决于“**每个请求者的身份验证”** 与当前MVPD关联的标记：

<!-- end list -->

1. 如果“每个请求者的身份验证”功能被禁用，则单个身份验证令牌将存储在全局粘贴板的本地；此令牌将在与当前MVPD集成的所有应用程序之间共享。
1. 如果启用了“每个请求者的身份验证”功能，则令牌将与执行身份验证流程的程序员明确关联（该令牌不会存储在全局粘贴板中，而是存储在仅对该程序员应用程序可见的专用文件中）。 更具体地说，将禁用不同应用程序之间的单点登录(SSO);用户在切换到新应用程序时需要显式地执行验证流程（前提是第二个应用程序的程序员与当前MVPD集成，并且本地缓存中不存在该程序员的验证令牌）。

 

#### 授权令牌

在任何给定时刻，AccessEnabler都只会缓存每个资源的一个授权令牌。 可以缓存多个授权令牌，但它们与不同资源相关联。 只要发出了新的授权令牌，并且旧的授权令牌已存在， *同一资源*，则新令牌将覆盖现有缓存值。

 

#### 媒体令牌

根本不应缓存短期媒体令牌。 每次调用授权API时，应从服务器中检索媒体令牌，因为该令牌仅限一次性使用。

 

### 持久性 {#persistence}

令牌需要在同一应用程序的连续运行中持续保留。 这意味着一旦获取了身份验证和授权令牌并且用户关闭了应用程序，则当用户重新打开应用程序时，应用程序将可以使用相同的令牌。 此外，这些令牌在多个应用程序中是持久的。 换言之，当用户使用一个应用程序通过特定身份提供者登录（成功获取身份验证和授权令牌）后，同一令牌可通过其他应用程序使用，并且当通过同一身份提供者登录时，不再提示用户输入凭据。 这种类型的无缝身份验证/授权工作流程使Primetime身份验证解决方案成为真正的TV-Everywhere实施。 

 

## iOS

iOS AccessEnabler库通过将令牌数据存储到称为的“剪贴板”数据结构中，来解决跨应用程序数据共享的问题 *粘贴板*. 此系统级别共享资源提供了关键要素，可用于实施所需的永久令牌用例：

- **支持结构化存储**  — 粘贴板不仅是简单的线性缓冲存储器结构。 它提供了类似词典的存储机制，该机制允许根据用户指定的键值进行数据索引。
- **支持使用基础文件系统的数据持久性**  — 粘贴板结构的内容可标记为永久性，在这种情况下，数据会保存在设备的内部内存中。

 

将特定令牌放入令牌缓存后，AccessEnabler库将在不同时间检查其有效性。  有效的令牌定义为：

- 令牌的TTL未过期。
- 令牌的颁发者包含在允许的身份提供程序列表中。

 

## tvOS

由于在tvOS上粘贴板不可用，因此tvOS AccessEnabler库使用NsUserDefaults作为存储选项。 这解决了持久保留身份验证和授权令牌的问题，但存储的信息无法在不同的应用程序之间共享。

 

**iOS 10粘贴板更改 —** 从以前版本的iOS升级时，粘贴板将被擦除。 这意味着所有应用程序都需要重新进行身份验证。

 

**iOS 7粘贴板更改 —** 由于粘贴板在iOS 7上的工作方式发生了更改，在iOS 7上运行的应用程序之间的跨单点登录(Cross SSO)将会受到限制。 具有该应用程序的应用程序 `<Bundle Seed ID>`(也称为 `<Team ID>`)将共享令牌，这意味着来自相同程序员X的应用程序A1和A2将共享令牌，而应用程序A1（程序员X）和应用程序A3（程序员Y）将不共享令牌。 

- 如果捆绑种子ID/团队ID是由同一配置文件生成的，则这2个应用程序之间的捆绑种子ID/团队ID是相同的。 有关更多信息，请访问此链接：
   [http://developer.apple.com/library/ios/\#documentation/general/conceptual/DevPedia-CocoaCore/AppID.html ](http://developer.apple.com/library/ios/#documentation/general/conceptual/DevPedia-CocoaCore/AppID.html)
- 无论使用何种Primetime身份验证SDK，iOS 7中都将存在这种“跨单点登录”限制。 

请阅读此技术说明，以了解有关在iOS 7和更高版本上配置单点登录（技术说明适用于Access Enabler v1.8和更高版本）的更多信息： <https://tve.zendesk.com/entries/58233434-Configuring-Pay-TV-pass-SSO-on-iOS>

 

### 令牌存储(AccessEnabler 1.7)

从AccessEnabler 1.7开始，令牌存储可以支持多个程序员 — MVPD组合，它依赖于可以容纳多个身份验证令牌的多级嵌套映射结构。 此新存储不会以任何方式影响AccessEnabler公共API，也不需要程序员进行更改。 以下示例说明了此新功能：

1. 打开App1（由Programmer1开发）。
1. 通过MVPD1（与Programmer1集成）进行身份验证。
1. 暂停/关闭当前应用程序，并打开App2（由Programmer2开发）。
1. 假设Programmer2未与MVPD2集成；因此，用户将不会在App2中进行身份验证。
1. 在App2中使用MVPD2（与Programmer2集成）进行身份验证。
1. 切换回App1；用户仍将通过Programmer1的身份验证。

在旧版AccessEnabler中，步骤6会将用户呈现为未验证的用户，因为令牌存储以前仅支持一个身份验证令牌。

 

从一个程序员/MVPD会话注销将清除整个底层存储，包括设备上所有其他程序员/MVPD身份验证令牌。 另一方面，取消身份验证流程(调用 [`setSelectedProvider(null)`](#setSelProv))不会清除底层存储，但只会影响当前程序员/MVPD身份验证尝试（通过清除当前程序员的MVPD）。

 

### 令牌导入器(AccessEnabler 1.7)

AccessEnabler 1.7中包含的另一个与存储相关的功能，使从旧存储区域导入身份验证令牌成为可能。 此“令牌导入器”有助于实现连续AccessEnabler版本之间的兼容性，从而即使在存储版本升级时也保持SSO状态。 导入器在 [`setRequestor()`](#setReq) 在以下两种情况下运行（假定当前存储中不存在当前程序员的有效身份验证令牌）：

- 由特定程序员开发的1.7应用程序的首次安装
- 将路径升级到将来使用新存储的AccessEnabler

导入操作对程序员是透明的，并且不需要在客户端应用程序中进行任何代码更改。

 

### 令牌整理程序(AccessEnabler 1.7.5)

从AccessEnabler 1.7.5转发，此服务在 [`setRequestor()`](#setReq)`. `它是由iOS 7从WiFi MAC地址切换到IDFA进行跟踪而开发的。 整理器可确保当前存储仅包含有效的身份验证令牌(根据设备ID(以前使用MAC地址计算，在iOS7之前)有效)。 令牌清理程序会删除所有无效的令牌。 

 

当在iOS 6上使用AccessEnabler 1.7.5应用程序，然后用户更新到iOS 7时，令牌整理程序服务非常有用。 此时，在iOS 6上获取的所有身份验证令牌都将无效(因为设备ID算法已从使用MAC地址更改为IDFA)。 清理器将清除所有无效的令牌，然后用户将未经身份验证。 

 

如果令牌清理程序不删除无效的令牌，则AccessEnabler将因身份验证令牌无效而无法获取授权。 这对最终用户来说将很难进行调试，因为授权错误消息可能是隐晦的，在确定导致问题的原因时不会过于有用。 

 

### 格式 {#format}

- [AuthN令牌](#authn_token)
- [AuthZ令牌](#authz_token)
- [短媒体令牌](#short_token)
- [设备绑定](#device_binding)


请注意，此处仅包含背景信息的AuthN和AuthZ令牌格式。 这些令牌的结构可随时通过Primetime身份验证进行更改。 由于AuthN和AuthZ令牌未在本地设备上公开，因此程序员无需知道AuthN和AuthZ令牌的确切结构即可实施其应用程序。 短媒体令牌 *is* 向程序员应用程序公开。

 

#### 身份验证令牌 {#authn_token}

下面列出了身份验证令牌的格式：

```
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

```
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
 

#### 短媒体令牌 {#short_token}

下面列出了短媒体令牌的格式。 此令牌会向程序员的应用程序公开。 在成功的授权过程结束时，该应用程序将基于程序员的应用程序：

```
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
 

### 设备绑定 {#device_binding}

在上面的XML列表中，请注意标有的标记 `simpleTokenFingerprint`. 此标记的用途是保存本机设备ID个性化信息。 AccessEnabler库能够获取此类个性化信息，并在授权调用期间将其提供给Primetime身份验证服务。 该服务将使用此信息并将其嵌入到实际的令牌中，从而有效地将令牌绑定到特定设备。 最终目标是使令牌不能跨设备转让。

 

由于这显然是一项与安全相关的功能，因此从安全角度来看，此信息具有内在的“敏感”性。 因此，需要保护这些信息，使其不受篡改和窃听。 通过通过HTTPS协议发送身份验证/授权请求，可解决窃听问题。 通过对设备标识信息进行数字签名来处理篡改保护。 AccessEnabler库根据设备提供的信息计算设备ID，然后将设备ID“清除”作为请求参数发送到Primetime身份验证服务器。 Primetime身份验证服务器使用Adobe的私钥对设备ID进行数字签名，并将其添加到返回到AccessEnabler的身份验证令牌中。 因此，设备ID与身份验证令牌绑定。 在授权流程中， AccessEnabler会再次以清除方式发送设备ID以及身份验证令牌。 验证过程失败会自动导致身份验证/授权工作流失败。 Primetime身份验证服务器将私钥应用于设备ID，并将其与身份验证令牌中的值进行比较。 如果二者不匹配，则授权流程将失败。

 

**AccessEnabler 1.7.5中的“设备绑定”说明：** 从AccessEnabler 1.7.5开始，计算设备ID的方式发生了变化，以便为iOS设备提供个性化信息。 此更改反映了iOS 7的更改：从iOS 7开始，Apple不再将WiFi MAC地址作为跟踪选项提供，改为提供其广告商标识符(IDFA)。 由于iOS 7上运行的应用程序的个性化信息基于IDFA，并且该信息会嵌入到权利流令牌中，这意味着此更改会对用户体验产生许多不同的可能影响。 不同的可能效果取决于用户从哪个iOS版本升级，以及程序员从哪个AccessEnabler版本升级。 有关此更改的详细信息，请参阅AccessEnabler SDK 1.7.5随附的发行说明。


## 相关信息 {#related}

<!--
- [iOS/tvOS Integration Cookbook](#)
- [iOS/tvOS API Reference](#)
- [Handling MVPDs with 'Not Trusted Certificates' in Primetime
  authentication native SDK (Tech Note)](#)
- [Registering Native Clients](#)
- [Generating Digital Certificates](#)
- [Understanding Tokens](#understanding_tokens)
- [Identifying Protected Resources](#)
- [SSO on iOS when using the Primetime authentication Access
  Enabler](#)
-->
