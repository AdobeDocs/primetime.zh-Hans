---
title: iOS/tvOS指南
description: iOS/tvOS指南
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2414'
ht-degree: 0%

---


# iOS/tvOS SDK指南 {#iostvos-sdk-cookbook}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## 简介 {#intro}

本文档介绍程序员的高级应用程序可以通过由iOS/tvOS AccessEnabler库公开的API来实施的授权工作流。

iOS/tvOS的Adobe Primetime身份验证授权解决方案最终分为两个域：

* UI域 — 这是实施UI并使用AccessEnabler库提供的服务提供对受限内容的访问的上层应用程序层。

* AccessEnabler域 — 在此域中，授权工作流以以下形式实施：

   * 对Adobe后端服务器进行的网络调用
   * 与身份验证和授权工作流相关的业务逻辑规则
   * 管理各种资源并处理工作流状态（如令牌缓存）

AccessEnabler域的目标是隐藏授权工作流的所有复杂性，并（通过AccessEnabler库）向上层应用程序提供一组简单的授权基元，您可以使用这些基元实施授权工作流：

1. 设置请求者身份
1. 针对特定身份提供者检查并获取身份验证
1. 检查并获取特定资源的授权
1. 注销
1. Apple通过支持Apple VSA框架来流动SSO

AccessEnabler的网络活动发生在其自己的线程中，因此UI线程从不被阻止。 因此，两个应用程序域之间的双向通信信道必须遵循完全异步模式：

* UI应用层通过AccessEnabler库公开的API调用，将消息发送到AccessEnabler域。
* AccessEnabler通过AccessEnabler协议中包含的回调方法响应UI层，UI层向AccessEnabler库注册该回调方法。

## 配置访客ID {#visitorIDSetup}

配置 [Marketing CloudvisitorID](https://marketing.adobe.com/resources/help/en_US/mcvid/) 从分析的角度来看，值非常重要。 设置visitorID值后，SDK将随每个网络调用发送此信息，Adobe Primetime身份验证服务器将收集此信息。 将来，您能够将来自Adobe Primetime身份验证服务的分析与来自其他应用程序或网站的任何其他分析报表相关联。 有关如何设置visitorID的信息可以找到 [此处](#setOptions).

## 权利流 {#entitlement}

A.  [先决条件](#prereqs) </br>
B.  [启动流程](#startup_flow) </br>
C.  [使用Apple SSO的身份验证流程](#authn_flow_wo_applesso)  </br>
D.  [iOS上使用Apple SSO的身份验证流程](#authn_flow_with_applesso) </br>
E.  [tvOS上使用Apple SSO的身份验证流程](#authn_flow_with_applesso_tvOS) </br>
F.  [授权流程](#authz_flow) </br>
G.  [查看媒体流量](#media_flow) </br>
H.  [注销流程(不使用Apple SSO)](#logout_flow_wo_AppleSSO) </br>
我。  [使用Apple SSO注销流程](#logout_flow_with_AppleSSO) </br>


### A.先决条件 {#prereqs}

1. 创建回调函数：
   * `setRequestorComplete()` </br>
   * 触发者 [setRequestor()](#$setReq)，则返回成功或失败。 </br>
   * 成功表示您可以继续进行授权调用。

   * [`displayProviderDialog(mvpds)`](#$dispProvDialog) </br>
      * 触发者 [`getAuthentication()`](#$getAuthN) 仅当用户尚未选择提供商(MVPD)且尚未进行身份验证时，才执行此操作。 </br>
      * 的 `mvpds` 参数是可供用户使用的提供程序数组。
   * `setAuthenticationStatus(status, errorcode)` </br>
      * 触发者 `checkAuthentication()` 每次。 </br>
      * 触发者 [`getAuthentication()`](#$getAuthN) 仅当用户已通过身份验证并选择了提供程序时。 </br>
      * 返回的状态是成功或失败，错误代码描述失败的类型。
   * [`navigateToUrl(url)`](#$nav2url) </br>
      * 触发者 [`getAuthentication()`](#$getAuthN) 用户选择MVPD后。 的 `url` 参数提供MVPD登录页面的位置。
   * `sendTrackingData(event, data)` </br>
      * 触发者 `checkAuthentication()`, [`getAuthentication()`](#$getAuthN), `checkAuthorization()`, [`getAuthorization()`](#$getAuthZ), `setSelectedProvider()`.
      * 的 `event` 参数指示发生了哪个授权事件；the `data` 参数是与事件相关的值列表。 
   * `setToken(token, resource)`

      * 触发者 [checkAuthorization()](#checkAuthZ) 和 [getAuthorization()](#$getAuthZ) 成功授权查看资源后。
      * 的 `token` 参数是短时的媒体令牌；the `resource` 参数是用户有权查看的内容。
   * `tokenRequestFailed(resource, code, description)` </br>
      * 触发者 [checkAuthorization()](#checkAuthZ) 和 [getAuthorization()](#$getAuthZ) 授权失败后。
      * 的 `resource` 参数是用户尝试查看的内容；the `code` 参数是指示发生哪种类型的故障的错误代码；the `description` 参数描述与错误代码关联的错误。
   * `selectedProvider(mvpd)` </br>
      * 触发者 [`getSelectedProvider()`](#getSelProv).
      * 的 `mvpd` 参数提供有关用户选择的提供程序的信息。
   * `setMetadataStatus(metadata, key, arguments)`
      * 触发者 `getMetadata().`
      * 的 `metadata` 参数提供您请求的特定数据；the `key` 参数是 [getMetadata()](#getMeta) 请求；和 `arguments` 参数是传递到的相同词典 [getMetadata()](#getMeta).
   * [&#39;preauthorizedResources(authorizedResources)&#39;](#preauthResources)

      * 触发者 [`checkPreauthorizedResources()`](#checkPreauth).

      * 的 `authorizedResources` 参数显示用户有权查看的资源。
   * [&#39;presentTvProviderDialog(viewController)&#39;](#presentTvDialog)

      * 触发者 [getAuthentication()](#getAuthN) 当当前请求者至少在具有SSO支持的MVPD上支持时。
      * viewController参数是Apple SSO对话框，需要在主视图控制器上显示。
   * [&#39;discessTvProviderDialog(viewController)&#39;](#dismissTvDialog)

      * 由用户操作触发(通过从Apple SSO对话框中选择“取消”或“其他电视提供商”)。
      * viewController参数是Apple SSO对话框，需要从主视图控制器中取消。











![](assets/iOS-flows.png)

### B.启动流程 {#startup_flow}

1. 启动高级应用程序。</br>
1. 启动Adobe Primetime身份验证 </br>

   a.调用 [`init`](#$init) 创建Adobe Primetime身份验证AccessEnabler的单个实例。
   * **依赖关系：** Adobe Primetime身份验证本机iOS/tvOS库(AccessEnabler)
   b.调用 `setRequestor()` 确定程序员的身份；程序员的通行证 `requestorID` 和（可选）Adobe Primetime身份验证端点数组。 对于tvOS，您还需要提供公钥和密钥。 请参阅 [无客户端文档](#create_dev) 以了解详细信息。

   * **依赖关系：** 有效的Adobe Primetime身份验证请求者ID(请与您的Adobe Primetime身份验证客户经理合作以安排此事)。

   * **触发器：**
      [setRequestorComplete()](#$setReqComplete) 回调。
   >[!NOTE]
   >
   >在请求者身份完全建立之前，无法完成授权请求。 这实际上意味着 [`setRequestor()`](#$setReq)  仍在运行，所有后续授权请求。 例如， [`checkAuthentication()`](#checkAuthN) 被阻止。

   您有两个实施选项：请求者标识信息被发送到后端服务器后，UI应用层可以选择以下两种方法之一： </br>

   1. 等待触发 [`setRequestorComplete()`](#setReqComplete) callback（AccessEnabler委托的一部分）。 此选项最确定地 [`setRequestor()`](#$setReq) 已完成，因此建议在大多数实施中使用。

   1. 继续，而不等待触发 [`setRequestorComplete()`](#setReqComplete) 回调，并开始发出授权请求。 这些调用（checkAuthentication、checkAuthorization、getAuthentication、getAuthorization、checkPreauthorizedResource、getMetadata、注销）由AccessEnabler库排队，该库将在 [`setRequestor()`](#$setReq). 例如，如果网络连接不稳定，此选项有时可能会中断。



1. 调用 `checkAuthentication()` 来检查现有的身份验证，而不启动完整的身份验证流程。  如果此调用成功，您可以直接转到授权流程。 如果没有，请继续执行身份验证流程。

   * **依赖关系：** 成功调用 [setRequestor()](#$setReq) （此依赖项也适用于所有后续调用）。

   * **触发器：** [setAuthenticationStatus()](#$setAuthNStatus) 回调。


### C.无Apple SSO的身份验证流程 {#authn_flow_wo_applesso}

1. 调用 [`getAuthentication()`](#$getAuthN) 启动身份验证流程，或获取用户已经进行身份验证的确认。

   **触发器：**

   * 的 [setAuthenticationStatus()](#$setAuthNStatus) 回调（如果用户已通过身份验证）。 在这种情况下，请直接转到 [授权流程](#authz_flow).

   * 的 [displayProviderDialog()](#$dispProvDialog) 回调（如果用户尚未进行身份验证）。

1. 向用户显示发送到的提供程序列表
   [`displayProviderDialog()`](#dispProvDialog).

1. 用户选择提供商后，从 `navigateToUrl:` 或 `navigateToUrl:useSVC:` 回调并打开 `UIWebView/WKWebView` 或 `SFSafariViewController` 控制器并将该控制器定向到URL。

1. 通过 `UIWebView/WKWebView` 或 `SFSafariViewController` 在上一步中实例化后，用户将登陆MVPD的登录页面并输入登录凭据。 控制器内进行了多个重定向操作。</br>

>[!NOTE]
>
>此时，用户有机会取消身份验证流程。 如果发生这种情况，您的UI层将负责通过调用将此事件通知AccessEnabler [setSelectedProvider()](#setSelProv) with `null` 作为参数。 这允许AccessEnabler清除其内部状态并重置身份验证流。

1. 用户成功登录后，应用程序层会检测特定自定义URL的加载情况。 请注意，此特定的自定义URL实际上无效，并且不希望控制器实际加载它。 它只能由您的应用程序解释为验证流程已完成并且关闭安全的信号 `UIWebView/WKWebView` 或 `SFSafariViewController` 控制器。 如果 `SFSafariViewController`控制器需要使用由 **`application's custom scheme`** (例如，`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`)，否则，此特定的自定义URL由 **`ADOBEPASS_REDIRECT_URL`** 常量(即 `adobepass://ios.app`)。

1. 关闭UIWebView/WKWebView或SFSafariViewController控制器并调用AccessEnabler的 `handleExternalURL:url` API方法，指示AccessEnabler从后端服务器检索身份验证令牌。

1. （可选）调用 [`checkPreauthorizedResources(resources)`](#$checkPreauth) 检查用户有权查看的资源。 的 `resources` 参数是与用户的身份验证令牌关联的受保护资源数组。 从用户的MVPD获取的授权信息的一个用途是装饰您的UI（例如，受保护内容旁边的锁定/解锁符号）。

   * **触发器：** [`preauthorizedResources()`](#preauthResources) 回调
   * **执行点：** 在完成身份验证流程之后

1. 如果身份验证成功，请转到授权流程。

### D.iOS上使用Apple SSO的身份验证流程 {#authn_flow_with_applesso}

1. 调用 [`getAuthentication()`](#$getAuthN) 启动身份验证流程，或获取用户已经进行身份验证的确认。
   **触发器：**

   * 的 [presentTvProviderDialog()](#presentTvDialog) 回调，如果用户未经身份验证，且当前请求者至少在支持SSO的MVPD上具有。 如果没有MVPD支持SSO，则将使用经典身份验证流程。

1. 在用户选择提供商后，AccessEnabler库将获取一个验证令牌，该令牌包含Apple VSA框架提供的信息。

1. 的 [setAuthenticationsStatus()](#setAuthNStatus) 将触发回调。 此时，用户应使用Apple SSO进行身份验证。

1. [可选] 调用 [`checkPreauthorizedResources(resources)`](#$checkPreauth) 检查用户有权查看的资源。 的 `resources` 参数是与用户的身份验证令牌关联的受保护资源数组。 从用户的MVPD获取的授权信息的一个用途是装饰您的UI（例如，受保护内容旁边的锁定/解锁符号）。

   * **触发器：** [`preauthorizedResources()`](#preauthResources) 回调
   * **执行点：** 在完成身份验证流程之后

1. 如果身份验证成功，请转到授权流程。

### E.在tvOS上使用Apple SSO的身份验证流程 {#authn_flow_with_applesso_tvOS}

1. 调用 [`getAuthentication()`](#$getAuthN) 启动身份验证流程，或获取用户已经进行身份验证的确认。
   **触发器：**
   * 的 [`presentTvProviderDialog()`](#presentTvDialog) 回调，如果用户未经身份验证，且当前请求者至少在支持SSO的MVPD上具有。 如果没有MVPD支持SSO，则将使用经典身份验证流程。

1. 用户选择提供商后， [`status()`](#status_callback_implementation) 将调用callback。 将提供注册代码，AccessEnabler库将开始轮询服务器以进行成功的第二次屏幕身份验证。

1. 如果提供的注册代码用于在第二个屏幕上成功进行身份验证，则 [`setAuthenticatiosStatus()`](#setAuthNStatus) 将触发回调。 此时，用户应使用Apple SSO进行身份验证。
1. [可选] 调用 [`checkPreauthorizedResources(resources)`](#$checkPreauth) 检查用户有权查看的资源。 的 `resources` 参数是与用户的身份验证令牌关联的受保护资源数组。 从用户的MVPD获取的授权信息的一个用途是装饰您的UI（例如，受保护内容旁边的锁定/解锁符号）。

   * **触发器：** [`preauthorizedResources()`](#preauthResources) 回调

   * **执行点：** 在完成身份验证流程之后
1. 如果身份验证成功，请转到授权流程。

### F.授权流程 {#authz_flow}

1. 调用 [getAuthorization()](#$getAuthZ) 启动授权流程。

   * **依赖关系：** 与MVPD商定的有效资源ID。
   * 资源ID应与在任何其他设备或平台上使用的ID相同，并且在MVPD中也将相同。 有关资源ID的信息，请参阅 [确定受保护的资源](/help/authentication/identify-protected-resources.md)

1. 验证身份验证和授权。

   * 如果 [getAuthorization()](#$getAuthZ) 调用成功：用户具有有效的AuthN和AuthZ令牌（用户已通过身份验证并有权观看请求的媒体）。

   * 如果 [getAuthorization()](#$getAuthZ) 失败：检查引发的异常以确定其类型（AuthN、AuthZ或其他内容）：
      * 如果是身份验证(AuthN)错误，则重新启动身份验证流程。
      * 如果是授权(AuthZ)错误，则用户无权观看请求的媒体，应向用户显示某种错误消息。
      * 如果存在其他类型的错误（连接错误、网络错误等） 然后向用户显示相应的错误消息。

1. 验证短媒体令牌。\
   使用Adobe Primetime身份验证媒体令牌验证器库来验证从 [getAuthorization()](#$getAuthZ) 上述调用：

   * 如果验证成功：为用户播放请求的媒体。
   * 如果验证失败：AuthZ令牌无效，应拒绝媒体请求，并向用户显示错误消息。


1. 返回到正常的应用程序流程。

### G.查看媒体流量 {#media_flow}

1. 用户选择要查看的媒体。
1. 介质是否受保护？ 您的应用程序会检查所选介质是否受到保护：

   * 如果选定的介质受到保护，应用程序将启动 [授权流程](#authz_flow) 上。

   * 如果所选媒体未受保护，则为用户播放该媒体。

### H.没有Apple SSO的注销流 {#logout_flow_wo_AppleSSO}

1. 调用 [`logout()`](#$logout) 将用户注销。 AccessEnabler会清除所有缓存的值和令牌。 清除缓存后， AccessEnabler会发起服务器调用以清理服务器端会话。 请注意，由于服务器调用可能导致到IdP的SAML重定向（这允许在IdP端清理会话），因此此调用必须遵循所有重定向。 因此，此调用必须在UIWebView/WKWebView或SFSafariViewController控制器内处理。

   a.按照与身份验证工作流相同的模式， AccessEnabler域通过 `navigateToUrl:` 或 `navigateToUrl:useSVC:` 回调，以创建UIWebView/WKWebView或SFSafariViewController控制器并指示加载回调中提供的URL `url` 参数。 这是后端服务器上注销端点的URL。

   b.您的应用程序必须监控 `UIWebView/WKWebView or SFSafariViewController` 控制器，并检测当它加载特定的自定义URL时（当它经过多个重定向时）。 请注意，此特定的自定义URL实际上无效，并且不希望控制器实际加载它。 它只能被您的应用程序解释为注销流程已完成并且关闭安全的信号 `UIWebView/WKWebView` 或 `SFSafariViewController` 控制器。 当控制器加载此特定的自定义URL时，您的应用程序必须关闭 `UIWebView/WKWebView or SFSafariViewController` 控制器并调用AccessEnabler的 `handleExternalURL:url`API方法。 如果 `SFSafariViewController`控制器需要使用由 **`application's custom scheme`** (例如， `adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`)，否则，此特定的自定义URL由 **`ADOBEPASS_REDIRECT_URL`**  常量(即 `adobepass://ios.app`)。

   >[!NOTE]
   >
   >注销流程与验证流程不同，因为用户无需以任何方式与UIWebView/WKWebView或SFSafariViewController进行交互。 UI应用程序层使用UIWebView/WKWebView或SFSafariViewController来确保遵循所有重定向。 因此，可以（并且建议）在注销过程中使控制器不可见（即隐藏）。


### I.使用Apple SSO注销流程 {#logout_flow_with_AppleSSO}

1. 调用 [`logout()`](#$logout) 将用户注销。
1. 的 [status()](#status_callback_implementation) 将使用VSA203调用callback。
1. 还应指示用户从系统设置登录。 如果失败，则在应用程序重新启动时，将导致重新验证。



<!--
### Related Information {#related}


- [iOS API Reference](#)

- [iOS Technical Overview](#)

- [Generating Digital Certificates](#)

- [Identifying Protected Resources](#)

- [Handling MVPDs with 'Not Trusted Certificates' in Adobe Primetime
  authentication native SDK (Tech Note)](#)

- [iOS Authentication error - adobepass.ios.app cannot be found (Tech
  Note)](#)
-->