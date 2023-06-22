---
title: Apple SSO指南(iOS/tvOS SDK)
description: Apple SSO指南(iOS/tvOS SDK)
exl-id: 2d59cd33-ccfd-41a8-9697-1ace3165bc44
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1867'
ht-degree: 0%

---

# Apple SSO指南(iOS/tvOS SDK) {#apple-sso-cookbook-iostvos-sdk}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权的使用。

## 介绍 {#Introduction}

Adobe Primetime Authentication AccessEnabler iOS/tvOS SDK可以通过我们所说的Apple SSO工作流程，为在iOS、iPadOS或tvOS上运行的客户端应用程序的最终用户支持平台单点登录(SSO)身份验证。

请注意，本文档是对现有AccessEnabler iOS/tvOS SDK文档的扩展，该文档可以找到 [此处](/help/authentication/iostvos-sdk-api-reference.md).

</br>

## 指南 {#Cookbook}

为了从Apple SSO用户体验中获益，一个应用程序需要集成AccessEnabler iOS/tvOS SDK，并遵循下面介绍的一系列提示。

</br>

### 先决条件 {#Prerequisites}

</br>

#### 权限

>[!TIP]
>
> **<u>专业提示：</u>** 要访问用户的订阅信息，用户必须向应用程序授予继续操作的权限，类似于提供对设备摄像头或麦克风的访问权限。 必须为每个应用程序请求此权限，设备将保存用户的选择。 请记住，用户可以通过转到应用程序设置（电视提供商权限访问）或转到以下部分来更改其决策： *`Settings -> TV Provider`* 在iOS/iPadOS上或 *`Settings -> Accounts -> TV Provider`* 在tvOS上。

>[!TIP]
>
> **<u>专业提示：</u>** 我们建议在应用程序进入前台状态时请求用户的权限，但这只是一个建议，因为应用程序可以检查 [访问权限](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) 用户在要求用户身份验证之前的任何时候的订阅信息。 此外，AccessEnabler iOS/tvOS SDK API将在需要时自动请求用户的权限。

>[!TIP]
>
> **<u>专业提示：</u>** 如果用户未授予其订阅信息的访问权限，或者如果与视频订阅者帐户框架的通信失败，则AccessEnabler iOS/tvOS SDK将回退到常规身份验证流程。

>[!TIP]
>
> **<u>专业提示：</u>** 我们建议解释单点登录(SSO)用户体验的好处，以激励拒绝授予访问订阅信息权限的用户。 请记住，用户可以通过转到应用程序设置（电视提供商权限访问）或转到以下部分来更改其决策： *`Settings -> TV Provider`* 在iOS/iPadOS上或 *`Settings -> Accounts -> TV Provider`* 在tvOS上。


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
> **<u>专业提示：</u>** 实施以下列表 [回调](/help/authentication/iostvos-sdk-api-reference.md) 这些特定于Apple SSO工作流程。

- [*presentTVProviderDialog*](/help/authentication/iostvos-sdk-api-reference.md#presenttvproviderdialog-presenttvdialog)  — 在Apple MVPD选取器即将打开时触发的回调。
- [*discissTVProviderDialog*](/help/authentication/iostvos-sdk-api-reference.md#dismisstvproviderdialog-dismisstvdialog)  — 在Apple MVPD选取器即将关闭时触发的回调。

</br>

#### 错误报告

>[!TIP]
>
> **<u>专业提示：</u>** 实施以下列表 [高级错误代码](/help/authentication/error-reporting.md) 这些特定于Apple SSO工作流程。

- ***N003***  — 用户从Apple MVPD选取器中选择了“其他电视提供商”选项。
- ***N004***  — 用户从Apple MVPD选取器中选择了一个当前请求者不支持的电视提供程序（集成或单点登录）。
- ***N005***  — 用户决定取消常规MVPD选取器或Apple MVPD选取器。
- ***VSA403***  — 应用程序的用户电视提供商权限被拒绝。
- ***VSA404***  — 应用程序的用户电视提供商权限未确定。
- ***VSA503***  — 视频订阅者帐户元数据请求失败，中提供了更多上下文 *消息* 字段。
- ***AAPL / APPL_ERROR***  — 视频订阅者帐户元数据请求失败，中提供了更多上下文 *详细信息* 字段。 

</br>

### 身份验证 {#Authentication}

>[!TIP]
>
> **<u>提示：</u>** 请按照以下步骤实施iOS/iPadOS/tvOS。

1. 应用程序必须 [初始化](/help/authentication/iostvos-sdk-api-reference.md#initsoftwarestatement-initwithsoftwarestatement) AccessEnabler iOS/tvOS SDK。
1. 应用程序必须 [设置当前请求者标识符](/help/authentication/iostvos-sdk-api-reference.md#setrequestorrequestorid-setrequestorrequestoridserviceproviders-setreqv3).

   **重要提示：** 第二步可能会触发 [高级错误代码](/help/authentication/error-reporting.md) 如果是，则特定于Apple SSO工作流程 **以下项之一为true**：

   - ***VSA403***  — 应用程序的用户电视提供商权限被拒绝。
   - ***VSA404***  — 应用程序的用户电视提供商权限未确定。
   - ***应用*** - AccessEnabler iOS/tvOS SDK与视频订阅者帐户框架之间的通信遇到错误。

   第二步将尝试静默地交换Apple SSO配置文件以获取Adobe身份验证令牌，以防出现以下情况 **以上都是假的** 和 **以下全部为true**：

   - 已为应用程序授予用户的TV提供商权限。
   - 用户已在设备系统级别登录其电视提供商帐户。
   - AccessEnabler iOS/tvOS SDK从视频订阅者帐户框架收到了用户的电视提供程序标识符。
   - 用户的电视提供程序与应用程序的集成可通过Adobe Primetime TVE仪表板启用。
   - 通过Adobe Primetime TVE功能板，可以使用该应用程序启用用户的电视提供商单点登录。
   - 用户的电视提供程序未通过Adobe Primetime TVE仪表板降级。
   - AccessEnabler iOS/tvOS SDK从视频订阅者帐户框架收到了用户的电视提供程序SAML响应。

   **<u>专业提示：</u>** 此第二步不会触发任何其他回调，但以下步骤除外 [setRequestorComplete](/help/authentication/iostvos-sdk-api-reference.md#setrequestorcomplete-setreqcomplete) callback，因为应用程序未显式启动身份验证。

1. 应用程序必须 [检查身份验证状态](/help/authentication/iostvos-sdk-api-reference.md#checkauthentication-checkauthn).

   **重要提示：** 此第三步可能会触发 [高级错误代码](/help/authentication/error-reporting.md) 如果是，则特定于Apple SSO工作流程 **以下项之一为true**：

   - ***VSA403**  — 用户在设备系统级别登录到其TV提供商帐户，但用户的TV提供商权限被拒绝用于该应用程序。
   - ***VSA404**  — 用户在设备系统级别登录到其TV提供商帐户，但用户的TV提供商权限对于应用程序尚未确定。
   - ***APPL\_ERROR**  — 用户在设备系统级别登录到其电视提供商帐户，但AccessEnabler iOS/tvOS SDK与视频订阅者帐户框架之间的通信遇到错误。

   **重要提示：** 此第三步将触发 [*setAuthenticationStatus*](/help/authentication/iostvos-sdk-api-reference.md#setauthenticationstatuserrorcode-setauthnstatus) 回调方式 *状态* 等于0，用例 **以下项之一为true**：

   - 用户未在设备系统级别或通过常规身份验证流程登录到其TV提供商帐户。
   - 用户在设备系统级别或通过常规身份验证流程登录到其电视提供程序帐户，但用户的电视提供程序身份验证令牌TTL已通过。
   - 用户在设备系统级别或通过常规身份验证流程登录到其电视提供程序帐户，但用户的电视提供程序与应用程序的集成已通过Adobe Primetime TVE仪表板禁用。
   - 用户已在设备系统级别登录其电视提供商帐户，但用户的电视提供商单点登录已通过Adobe Primetime TVE仪表板禁用该应用程序。
   - 用户在设备系统级别登录到其TV提供商帐户，但用户的TV提供商权限被拒绝用于该应用程序。
   - 用户在设备系统级别登录到其TV提供商帐户，但用户的TV提供商权限对于应用程序尚未确定。
   - 用户在设备系统级别登录到其电视提供商帐户，但AccessEnabler iOS/tvOS SDK与视频订阅者帐户框架之间的通信遇到错误。

   **重要提示：** 此第三步将触发 [*setAuthenticationStatus*](/help/authentication/iostvos-sdk-api-reference.md#setauthenticationstatuserrorcode-setauthnstatus) 回调方式 *状态* 等于1，如果是 **上述所有说法都是错误的。**


1. 应用程序必须 [初始化身份验证](/help/authentication/iostvos-sdk-api-reference.md#getauthentication-getauthenticationwithdata-getauthn) 如果以前的身份验证状态检查触发了 [*setAuthenticationStatus*](/help/authentication/iostvos-sdk-api-reference.md#setauthenticationstatuserrorcode-setauthnstatus) 回调方式 *状态* 等于0。

   **<u>专业提示：</u>** 实施以下AccessEnabler iOS/tvOS SDK API之一 [getAuthentication](/help/authentication/iostvos-sdk-api-reference.md#getAuthN) 或 [getAuthentication：filter](/help/authentication/iostvos-sdk-api-reference.md#getAuthN_filter).

   **重要提示：** 这第四步可能会触发 [高级错误代码](/help/authentication/error-reporting.md) 如果是，则特定于Apple SSO工作流程 **以下项之一为true**：

   - ***VSA403***  — 应用程序的用户电视提供商权限被拒绝。
   - ***VSA404***  — 应用程序的用户电视提供商权限未确定。
   - ***VSA503*** - AccessEnabler iOS/tvOS SDK与视频订阅者帐户框架之间的通信遇到错误。
   - ***N003***  — 用户从Apple MVPD选取器中选择了“其他电视提供商”选项。
   - ***N004***  — 用户从Apple MVPD选取器中选择了一个当前请求者不支持的电视提供程序（集成或单点登录）。
   - ***N005***  — 用户决定取消常规MVPD选取器或Apple MVPD选取器。

   **重要提示：** 第四步将回退到常规身份验证流程，触发 [displayProviderDialog](/help/authentication/iostvos-sdk-api-reference.md#dispProvDialog) 回调和 **一** 以上的 [高级错误代码](/help/authentication/error-reporting.md)，以防万一 **以上任一情况为真**. 

   **重要提示：** 第四步将回退到常规身份验证流程，触发 [navigateToUrl](/help/authentication/iostvos-sdk-api-reference.md#nav2url) 或 [navigateToUrl：useSVC](/help/authentication/iostvos-sdk-api-reference.md#nav2urlSVC) 回调和 **无** 以上的 [高级错误代码](/help/authentication/error-reporting.md)，如果用户选择的电视提供程序不支持Apple SSO，但存在于Apple MVPD选取器中。

   **<u>专业提示：</u>** AccessEnabler iOS/tvOS SDK以静默方式调用 [setSelectedProvder](/help/authentication/iostvos-sdk-api-reference.md#setSelProv) API，以防用户选择了不支持Apple SSO，但存在于Apple MVPD选取器中的电视提供商。

   **重要提示：** 第四步将尝试静默地将Apple SSO配置文件交换为Adobe身份验证令牌，以防出现以下情况 **以上都是假的** 和 **以下全部为true**：

   - 已为应用程序授予用户的TV提供商权限。
   - 用户已登录/当前已在设备系统级别登录其电视提供商帐户。
   - AccessEnabler iOS/tvOS SDK从视频订阅者帐户框架收到了用户的电视提供程序标识符。
   - 用户的电视提供程序与应用程序的集成可通过Adobe Primetime TVE仪表板启用。
   - 通过Adobe Primetime TVE功能板，可以使用该应用程序启用用户的电视提供商单点登录。
   - 用户的电视提供程序未通过Adobe Primetime TVE仪表板降级。
   - AccessEnabler iOS/tvOS SDK从视频订阅者帐户框架收到了用户的电视提供程序SAML响应。


 

>**<u>专业提示：</u>** 第四步将触发 [*setAuthenticationStatus*](/help/authentication/iostvos-sdk-api-reference.md#setAuthNStatus) callback，不考虑 *状态* 结果，因为身份验证是由应用程序显式启动的。


</br>

### 元数据 {#Metadata}

应用程序可以选择确定是否由于通过平台SSO登录而发生了身份验证，请使用“*tokenSource``* [用户元数据](/help/authentication/iostvos-sdk-api-reference.md#getMeta) AccessEnabler iOS/tvOS SDK中的API。

```swift
    ...
    accessEnabler.getMetadata([METADATA_OPCODE_KEY:Int(METADATA_USER_META), METADATA_USER_META_KEY: "tokenSource"])
    ...
```

</br>

### 注销 {#Logout}

此 [视频订阅者帐户](https://developer.apple.com/documentation/videosubscriberaccount) 框架不提供API以编程方式注销在设备系统级别登录到其电视提供商帐户的人员。 因此，要使注销完全生效，最终用户必须明确从中注销 *`Settings -> TV Provider`* 在iOS/iPadOS上或 *`Settings -> Accounts -> TV Provider`* 在tvOS上。 用户将拥有的另一个选项是从特定应用程序设置部分（TV提供商权限访问）撤销访问用户订阅信息的权限。

>[!TIP]
>
> **<u>提示：</u>** 通过AccessEnabler iOS/tvOS SDK媒体实施此功能 [注销](/help/authentication/iostvos-sdk-api-reference.md#logout) API。


>[!TIP]
>
> **<u>专业提示：</u>** 请按照以下步骤实施tvOS。

- 应用程序必须 [启动注销](/help/authentication/iostvos-sdk-api-reference.md#logout) 从AccessEnabler iOS/tvOS SDK访问。 这不利于清理MVPD端的会话。
- 应用程序必须指示/提示用户明确从中注销 *`Settings -> Accounts -> TV Provider`* 仅在tvOS上 [*VSA203* 状态代码已触发](/help/authentication/error-reporting.md).

>[!TIP]
>
> **<u>专业提示：</u>** 请按照以下步骤实施iOS/iPadOS。

- 应用程序必须 [启动注销](/help/authentication/iostvos-sdk-api-reference.md#logout) 从AccessEnabler iOS/tvOS SDK访问。 这将有助于MVPD端的会话清理。
- 应用程序必须指示/提示用户明确从中注销 *`Settings -> TV Provider`* 仅在iOS/iPadOS上 [*VSA203* 状态代码已触发](/help/authentication/error-reporting.md).


<!--
## Resources {#Resources}

- [Apple SSO Overview](/help/authentication/apple-sso-overview.md)
- [AccessEnabler iOS/tvOS SDK Overview](/help/authentication/iostvos-sdk-overview.md)
- [AccessEnabler iOS/tvOS SDK Cookbook](/help/authentication/iostvos-sdk-cookbook.md)
- [AccessEnabler iOS/tvOS SDK API Reference](/help/authentication/iostvos-sdk-api-reference.md)
- [Error Reporting](/help/authentication/error-reporting.md)
- [Apple Developer Documentation - Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount)
-->
