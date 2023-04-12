---
title: Apple SSO指南(iOS/tvOS SDK)
description: Apple SSO指南(iOS/tvOS SDK)
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1867'
ht-degree: 0%

---



# Apple SSO指南(iOS/tvOS SDK) {#apple-sso-cookbook-iostvos-sdk}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## 简介 {#Introduction}

Adobe Primetime Authentication AccessEnabler iOS/tvOS SDK可通过我们称为Apple SSO工作流，为在iOS、iPadOS或tvOS上运行的客户端应用程序的最终用户支持平台单点登录(SSO)身份验证。

请注意，本文档是对现有AccessEnabler iOS/tvOS SDK文档的扩展，可在 [此处](/help/authentication/iostvos-sdk-api-reference.md).

</br>

## 指南 {#Cookbook}

为了从Apple SSO用户体验中受益，一个应用程序需要集成AccessEnabler iOS/tvOS SDK，并按照下面提供的提示序列操作。

</br>

### 先决条件 {#Prerequisites}

</br>

#### 权限

>[!TIP]
>
> **<u>专业提示：</u>** 为了能够访问用户的订阅信息，用户必须授予应用程序继续操作的权限，这与提供对设备的摄像头或麦克风的访问权限类似。 必须根据应用程序请求此权限，设备将保存用户的选择。 请记住，用户可以通过转到应用程序设置（电视提供商权限访问）或 *`Settings -> TV Provider`* 在iOS/iPadOS或 *`Settings -> Accounts -> TV Provider`* 在tvOS上。

>[!TIP]
>
> **<u>专业提示：</u>** 我们建议在应用程序进入前台状态时请求用户的权限，但这只是建议，因为应用程序可以检查 [访问权限](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) 用户在要求用户进行身份验证之前的任意时间点的订阅信息。 此外， AccessEnabler iOS/tvOS SDK API将在需要时自动请求用户的权限。

>[!TIP]
>
> **<u>专业提示：</u>** 如果用户未授予对订阅信息的访问权限，或者与视频订阅者帐户框架的通信失败，则AccessEnabler iOS/tvOS SDK将回退到常规身份验证流程。

>[!TIP]
>
> **<u>专业提示：</u>** 我们建议通过解释单点登录(SSO)用户体验的好处，来激励拒绝授予访问订阅信息权限的用户。 请记住，用户可以通过转到应用程序设置（电视提供商权限访问）或 *`Settings -> TV Provider`* 在iOS/iPadOS或 *`Settings -> Accounts -> TV Provider`* 在tvOS上。


```swift
    ...
    let videoSubscriberAccountManager: VSAccountManager = VSAccountManager();
    
    videoSubscriberAccountManager.checkAccessStatus(options: [VSCheckAccessOption.prompt: true]) { (accessStatus, error) -> Void in
                switch (accessStatus) {
                // The user allows the application to access subscription information.
                case VSAccountAccessStatus.granted:
                   // Do nothing.
                
                // The user has not yet made a choice or does not allow the application to access subscription information.
                default:
                   // Incentivize users who refuse to give permission to access subscription information by explaining the benefits of the Single Sign-On (SSO) user experience. Please bear in mind that the user can change its decision by going to the application settings (TV Provider permission access) or to the section from Settings -> TV Provider on iOS/iPadOS or Settings -> Accounts -> TV Provider on tvOS.
                   ...
                }
    }
    ... 
```

</br>

#### 回调

>[!TIP]
>
> **<u>专业提示：</u>** 实施以下列表 [回调](/help/authentication/iostvos-sdk-api-reference.md) 特定于Apple SSO工作流。

- [*presentTVProviderDialog*](/help/authentication/iostvos-sdk-api-reference.md#presenttvproviderdialog-presenttvdialog)  — 当Apple MVPD选取器打开时触发回调。
- [*discessTVProviderDialog*](/help/authentication/iostvos-sdk-api-reference.md#dismisstvproviderdialog-dismisstvdialog)  — 当Apple MVPD选取器要关闭时触发回调。

</br>

#### 错误报告

>[!TIP]
>
> **<u>专业提示：</u>** 实施以下列表 [高级错误代码](/help/authentication/error-reporting.md) 特定于Apple SSO工作流。

- ***N003***  — 用户从Apple MVPD选取器中选择了“其他电视提供商”选项。
- ***N004***  — 用户从Apple MVPD选取器中选择了电视提供商，当前请求者不支持该选取器（集成或单点登录已禁用）。
- ***N005***  — 用户决定取消常规的MVPD选取器或Apple MVPD选取器。
- ***VSA403***  — 拒绝用户对应用程序的电视提供商权限。
- ***VSA404***  — 用户的电视提供商权限对应用程序未确定。
- ***VSA503***  — 视频订阅者帐户元数据请求失败， *消息* 字段。
- ***AAPL / APPL_ERROR***  — 视频订阅者帐户元数据请求失败， *详细信息* 字段。 

</br>

### 身份验证 {#Authentication}

>[!TIP]
>
> **<u>提示：</u>** 请按照以下步骤执行iOS/iPadOS/tvOS实施。

1. 申请必须 [初始化](/help/authentication/iostvos-sdk-api-reference.md#initsoftwarestatement-initwithsoftwarestatement) accessEnabler iOS/tvOS SDK。
1. 申请必须 [设置当前请求者标识符](/help/authentication/iostvos-sdk-api-reference.md#setrequestorrequestorid-setrequestorrequestoridserviceproviders-setreqv3).

   **重要信息：** 第二步可能会触发 [高级错误代码](/help/authentication/error-reporting.md) 特定于Apple SSO工作流(在 **以下任一情况为true**:

   - ***VSA403***  — 拒绝用户对应用程序的电视提供商权限。
   - ***VSA404***  — 用户的电视提供商权限对应用程序未确定。
   - ***APPL*** - AccessEnabler iOS/tvOS SDK与视频订阅者帐户框架之间的通信遇到错误。

   第二步将尝试静默地将Apple SSO配置文件交换为Adobe身份验证令牌，以防 **以上所有的都是假的** 和 **以下所有情况都是真的**:

   - 将为应用程序授予用户的电视提供商权限。
   - 用户在设备系统级别登录到其电视提供商帐户。
   - AccessEnabler iOS/tvOS SDK从视频订阅者帐户框架中接收了用户的电视提供商标识符。
   - 通过Adobe Primetime TVE功能板，实现了用户与应用程序的电视提供商集成。
   - 通过Adobe Primetime TVE功能板启用用户与应用程序的电视提供商单点登录。
   - 用户的电视提供商未通过Adobe Primetime TVE功能板降级。
   - AccessEnabler iOS/tvOS SDK从视频订阅者帐户框架中接收了用户的电视提供商SAML响应。

   **<u>专业提示：</u>** 除了 [setRequestorComplete](/help/authentication/iostvos-sdk-api-reference.md#setrequestorcomplete-setreqcomplete) 回调，因为应用程序未明确启动身份验证。

1. 申请必须 [检查身份验证状态](/help/authentication/iostvos-sdk-api-reference.md#checkauthentication-checkauthn).

   **重要信息：** 第三步可能会触发 [高级错误代码](/help/authentication/error-reporting.md) 特定于Apple SSO工作流(在 **以下任一情况为true**:

   - ***VSA403**  — 用户已在设备系统级别登录到其电视提供商帐户，但拒绝用户对该应用程序的电视提供商权限。
   - ***VSA404**  — 用户已在设备系统级别登录到其电视提供商帐户，但用户对应用程序的电视提供商权限不确定。
   - ***APPL\_ERROR**  — 用户已在设备系统级别登录到其电视提供商帐户，但AccessEnabler iOS/tvOS SDK与视频订阅者帐户框架之间的通信遇到错误。

   **重要信息：** 第三步将触发 [*setAuthenticationStatus*](/help/authentication/iostvos-sdk-api-reference.md#setauthenticationstatuserrorcode-setauthnstatus) 回调 *状态* 等于0，在情况下 **以下任一情况为true**:

   - 用户未在设备系统级别或通过常规身份验证流程登录到其电视提供商帐户。
   - 用户在设备系统级别或通过常规身份验证流程登录到其电视提供商帐户，但用户的电视提供商身份验证令牌TTL已通过。
   - 用户在设备系统级别或通过常规身份验证流程登录到其电视提供商帐户，但用户与应用程序的电视提供商集成会通过Adobe Primetime TVE仪表板被禁用。
   - 用户在设备系统级别登录到其电视提供商帐户，但通过Adobe Primetime TVE功能板禁用用户与应用程序的电视提供商单点登录。
   - 用户已在设备系统级别登录到其电视提供商帐户，但拒绝用户对该应用程序的电视提供商权限。
   - 用户已在设备系统级别登录到其电视提供商帐户，但用户对应用程序的电视提供商权限不确定。
   - 用户已在设备系统级别登录到其电视提供商帐户，但AccessEnabler iOS/tvOS SDK与视频订阅者帐户框架之间的通信遇到错误。

   **重要信息：** 第三步将触发 [*setAuthenticationStatus*](/help/authentication/iostvos-sdk-api-reference.md#setauthenticationstatuserrorcode-setauthnstatus) 回调 *状态* 等于1，如果为 **以上所有内容都是假的。**


1. 申请必须 [初始化身份验证](/help/authentication/iostvos-sdk-api-reference.md#getauthentication-getauthenticationwithdata-getauthn) 如果之前的身份验证状态检查触发了 [*setAuthenticationStatus*](/help/authentication/iostvos-sdk-api-reference.md#setauthenticationstatuserrorcode-setauthnstatus) 回调 *状态* 等于0。

   **<u>专业提示：</u>** 实施以下任一AccessEnabler iOS/tvOS SDK API [getAuthentication](/help/authentication/iostvos-sdk-api-reference.md#getAuthN) 或 [getAuthentication:filter](/help/authentication/iostvos-sdk-api-reference.md#getAuthN_filter).

   **重要信息：** 第四步可能会触发 [高级错误代码](/help/authentication/error-reporting.md) 特定于Apple SSO工作流(在 **以下任一情况为true**:

   - ***VSA403***  — 拒绝用户对应用程序的电视提供商权限。
   - ***VSA404***  — 用户的电视提供商权限对应用程序未确定。
   - ***VSA503*** - AccessEnabler iOS/tvOS SDK与视频订阅者帐户框架之间的通信遇到错误。
   - ***N003***  — 用户从Apple MVPD选取器中选择了“其他电视提供商”选项。
   - ***N004***  — 用户从Apple MVPD选取器中选择了电视提供商，当前请求者不支持该选取器（集成或单点登录已禁用）。
   - ***N005***  — 用户决定取消常规的MVPD选取器或Apple MVPD选取器。

   **重要信息：** 第四步将通过触发 [displayProviderDialog](/help/authentication/iostvos-sdk-api-reference.md#dispProvDialog) 回调和 **one** 的 [高级错误代码](/help/authentication/error-reporting.md)，在 **以上其中之一是真的**. 

   **重要信息：** 第四步将通过触发 [navigateToUrl](/help/authentication/iostvos-sdk-api-reference.md#nav2url) 或 [navigateToUrl:useSVC](/help/authentication/iostvos-sdk-api-reference.md#nav2urlSVC) 回调和 **无** 的 [高级错误代码](/help/authentication/error-reporting.md)，以防用户选择不支持Apple SSO但Apple MVPD选取器中存在的电视提供商。

   **<u>专业提示：</u>** AccessEnabler iOS/tvOS SDK会静默调用 [setSelectedProvder](/help/authentication/iostvos-sdk-api-reference.md#setSelProv) API，用户选择的电视提供商不支持Apple SSO，但Apple MVPD选取器中存在API。

   **重要信息：** 此第四步将尝试静默地将Apple SSO配置文件交换为Adobe身份验证令牌，以防 **以上所有的都是假的** 和 **以下所有情况都是真的**:

   - 将为应用程序授予用户的电视提供商权限。
   - 用户已登录/当前已登录到设备系统级别的电视提供商帐户。
   - AccessEnabler iOS/tvOS SDK从视频订阅者帐户框架中接收了用户的电视提供商标识符。
   - 通过Adobe Primetime TVE功能板，实现了用户与应用程序的电视提供商集成。
   - 通过Adobe Primetime TVE功能板启用用户与应用程序的电视提供商单点登录。
   - 用户的电视提供商未通过Adobe Primetime TVE功能板降级。
   - AccessEnabler iOS/tvOS SDK从视频订阅者帐户框架中接收了用户的电视提供商SAML响应。


 

>**<u>专业提示：</u>** 第四个步骤将触发 [*setAuthenticationStatus*](/help/authentication/iostvos-sdk-api-reference.md#setAuthNStatus) 回调，不考虑 *状态* 结果，因为身份验证是由应用程序明确启动的。


</br>

### 元数据 {#Metadata}

应用程序可以选择使用“*tokenSource&quot;* [用户元数据](/help/authentication/iostvos-sdk-api-reference.md#getMeta) AccessEnabler iOS/tvOS SDK中的API。

```swift
    ...
    accessEnabler.getMetadata([METADATA_OPCODE_KEY:Int(METADATA_USER_META), METADATA_USER_META_KEY: "tokenSource"])
    ...
```

</br>

### 注销 {#Logout}

的 [视频订阅者帐户](https://developer.apple.com/documentation/videosubscriberaccount) 框架不提供API，以编程方式注销在设备系统级别登录到其电视提供商帐户的人员。 因此，要使注销完全生效，最终用户必须明确地从中注销 *`Settings -> TV Provider`* 在iOS/iPadOS或 *`Settings -> Accounts -> TV Provider`* 在tvOS上。 用户必须从特定应用程序设置部分（电视提供商权限访问）中撤消访问用户订阅信息的权限。

>[!TIP]
>
> **<u>提示：</u>** 通过AccessEnabler iOS/tvOS SDK媒介实施此功能 [注销](/help/authentication/iostvos-sdk-api-reference.md#logout) API。


>[!TIP]
>
> **<u>专业提示：</u>** 请按照以下步骤实施tvOS。

- 申请必须 [启动注销](/help/authentication/iostvos-sdk-api-reference.md#logout) 从AccessEnabler iOS/tvOS SDK中。 这不利于MVPD端的会话清理。
- 应用程序必须指示/提示用户明确从中注销 *`Settings -> Accounts -> TV Provider`* （仅在大小写时） [*VSA203* 状态代码已触发](/help/authentication/error-reporting.md).

>[!TIP]
>
> **<u>专业提示：</u>** 请按照以下步骤对iOS/iPadOS实施进行操作。

- 申请必须 [启动注销](/help/authentication/iostvos-sdk-api-reference.md#logout) 从AccessEnabler iOS/tvOS SDK中。 这将有助于在MVPD端进行会话清理。
- 应用程序必须指示/提示用户明确从中注销 *`Settings -> TV Provider`* 在iOS/iPadOS上，以防万一 [*VSA203* 状态代码已触发](/help/authentication/error-reporting.md).


<!--
## Resources {#Resources}

- [Apple SSO Overview](/help/authentication/apple-sso-overview.md)
- [AccessEnabler iOS/tvOS SDK Overview](/help/authentication/iostvos-sdk-overview.md)
- [AccessEnabler iOS/tvOS SDK Cookbook](/help/authentication/iostvos-sdk-cookbook.md)
- [AccessEnabler iOS/tvOS SDK API Reference](/help/authentication/iostvos-sdk-api-reference.md)
- [Error Reporting](/help/authentication/error-reporting.md)
- [Apple Developer Documentation - Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount)
-->
