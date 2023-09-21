---
title: Apple SSO概述
description: Apple SSO概述
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1452'
ht-degree: 0%

---

# Apple SSO概述 {#apple-sso-overview}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权使用。

## 介绍 {#Introduction}

Apple提供了一个API，允许用户在设备系统级别登录其电视提供商帐户，而无需逐个应用程序进行身份验证。

因此，Apple与Adobe Primetime身份验证合作，在iPhone、iPad和Apple电视的所有者的TV Everywhere生态系统中创建Platform Single Sign-On (SSO)用户体验。

为了从Apple设备上的单点登录(SSO)用户体验中获益，必须完成一系列先决条件。

</br>

## 先决条件 {#Prerequisites}

前提条件可能适用于TVE业务中涉及的一个或多个实体，例如程序员、MVPD、Adobe Primetime身份验证或Apple。

</br>

### 程序员 {#Programmer}

为了从单点登录(SSO)用户体验中获益，一位程序员必须：

1. 请至少使用Xcode版本8和iOS/tvOS版本10。

1. 拥有 [视频订阅者单点登录授权](https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_developer_video-subscriber-single-sign-on) 已配置为使用他们的Apple开发人员帐户。 请联系Apple以启用 [视频订阅者帐户框架](https://developer.apple.com/documentation/videosubscriberaccount) 作为您的Apple团队ID。

1. 通过，为每个所需的集成(Channel x MVPD)和所需的平台(iOS/tvOS)启用单点登录（是） [Adobe Primetime TVE功能板](https://console.auth.adobe.com/).

1. 使用Apple身份验证团队提供的以下两个解决方案之一集成Adobe Primetime SSO工作流：

   - Adobe Primetime身份验证REST API可为在iOS、iPadOS或tvOS上运行的客户端应用程序的最终用户支持平台单点登录(SSO)身份验证。 另请参阅 [Apple SSO指南(REST API)](/help/authentication/apple-sso-cookbook-rest-api.md).

   - Adobe Primetime Authentication AccessEnabler iOS/tvOS SDK可为在iOS、iPadOS或tvOS上运行的客户端应用程序的最终用户支持平台单点登录(SSO)身份验证。 另请参阅 [Apple SSO指南(iOS/tvOS SDK)](/help/authentication/apple-sso-cookbook-iostvos-sdk.md).

   - **<u>专业提示：</u>** 要访问用户的订阅信息，用户必须向应用程序授予继续操作的权限，类似于提供对设备摄像头或麦克风的访问权限。 必须为每个应用程序请求此权限，设备将保存用户的选择。 请记住，用户可以通过转到应用程序设置（电视提供商权限访问）或部分，更改其决策 *`Settings -> TV Provider`* 在iOS/iPadOS上，或 *`Settings -> Accounts -> TV Provider`* 在tvOS上。

   - **<u>专业提示：</u>** 我们建议在应用程序进入前台状态时请求用户的权限，但这只是一个建议，因为应用程序可以检查 [访问权限](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) 用户在要求用户身份验证之前的任何时候的订阅信息。 此外，AccessEnabler iOS/tvOS SDK API将在需要时自动请求用户的权限。

   - **<u>专业提示：</u>** 我们建议通过解释单点登录(SSO)用户体验的好处，鼓励拒绝授予访问订阅信息权限的用户。 请记住，用户可以通过转到应用程序设置（电视提供商权限访问）或部分，更改其决策 *`Settings -> TV Provider`* 在iOS/iPadOS上，或 *`Settings -> Accounts -> TV Provider`* 在tvOS上。

这样产生的结果应会创建符合以下用户流程的体验，我们建议您在开始开发应用程序之前查阅这些用户流程：

- [IPHONE / IPAD](http://tve.zendesk.com/hc/article_attachments/205624966/User_flows_AppleSSO_iOS_v2.pdf) 用户流
- [APPLE TV](http://tve.zendesk.com/hc/article_attachments/206669126/User_flows_tvOS.pdf) 用户流


>[!IMPORTANT]
>
> 单点登录功能为 **已启用** 适用于iOS/tvOS的 **和** 就Apple而言 **已载入（支持）或选取器** MVPD来自Apple SSO工作流的身份验证/注销流将同时涉及Apple和Adobe Primetime身份验证解决方案，而所有其他流（授权、预授权、元数据等） 将仅由Adobe Primetime身份验证提供服务。


>[!IMPORTANT]
>
> 单点登录功能为 **已禁用** 适用于iOS/tvOS的 **或** 就Apple而言 **未载入（不支持）** MVPDs身份验证/注销流将从Apple SSO工作流回退到仅由Adobe Primetime身份验证提供服务的常规工作流。


>[!IMPORTANT]
>
> Apple Apple SSO工作流程的一个主要收益由一个屏幕身份验证用户流表示，当单点登录功能为 **已启用** 适用于tvOS的 **和** 就Apple而言 **已载入（支持）** MVPDs。


### MVPD {#MVPD}

为了从单点登录(SSO)用户体验中获益，一个MVPD必须：



1. 被载入Apple的Apple SSO工作流。 请联系Apple以简化入门培训流程。
1. 提供一个能够处理用户登录表单的JavaScript TVML应用程序。 请联系Apple以接收正确的文档。
1. 提供一个字符串值，表示Apple在新用户引导过程中分配的提供商标识符。 请联系Adobe Primetime身份验证以执行配置更改。

</br>

## 常见问题解答 {#FAQ}

1. 如果Apple SSO工作流出现问题，使用AccessEnabler iOS/tvOS SDK的应用程序能否回退到常规身份验证流程？
   - 这是可能的，但需要对 [Adobe Primetime TVE功能板](https://console.auth.adobe.com/). 此 *启用单点登录* 必须设置为 *否* (Channel x MVPD)和所需的平台(iOS/tvOS)进行集成。
   - 应用程序仅在调用后确认配置更改 [setRequestor](/help/authentication/iostvos-sdk-api-reference.md#setReqV3) API，以防它使用AccessEnabler iOS/tvOS SDK。
1. 当通过其他设备或其他应用程序上的平台SSO登录后，应用程序是否知道发生了身份验证？
   - 此信息将不可用。
1. 由于通过同一设备上的平台SSO登录，应用程序是否知道何时发生身份验证？
   - 此信息作为用户元数据键的一部分提供： *tokenSource*，在此例中，应当返回字符串值“Apple”。
1. 如果用户登录到 *`Settings -> TV Provider`* 在iOS/iPadOS上，或 *`Settings -> Accounts -> TV Provider`* 在tvOS部分使用未与应用程序集成的MVPD？
   - 当用户启动应用程序时，将无法通过Apple SSO工作流对用户进行身份验证。 因此，应用程序必须回退到常规身份验证流程，并显示自己的MVPD选取器。
1. 如果用户登录到 *`Settings -> TV Provider`* 在iOS/iPadOS上，或 *`Settings -> Accounts -> TV Provider`* 在tvOS部分中，使用 *启用单点登录* 设置于 *否* 在 [Adobe Primetime TVE功能板](https://console.auth.adobe.com/) 用于iOS/tvOS平台？
   - 当用户启动应用程序时，将无法通过Apple SSO工作流对用户进行身份验证。 因此，应用程序必须回退到常规身份验证流程，并显示自己的MVPD选取器。
1. 如果用户具有不受Apple载入（不支持）但存在于Apple选取器中的MVPD，会发生什么情况？
   - 当用户启动应用程序时，用户将仅通过Apple SSO工作流选择MVPD，而不完成身份验证流程。 因此，应用程序必须回退到常规身份验证流程，但可以使用已选择的MVPD。
1. 如果用户具有Apple未载入（不支持）的MVPD，会发生什么情况？
   - 当用户启动应用程序时，将通过Apple SSO工作流选择“其他电视提供商”选取器选项。 因此，应用程序必须回退到常规身份验证流程，并显示自己的MVPD选取器。
1. 如果用户的MVPD通过介质降级，会发生什么情况 [Adobe Primetime TVE功能板](https://console.auth.adobe.com/)？
   - 当用户启动应用程序时，将通过降级机制而不是通过Apple SSO工作流对用户进行身份验证。
   - 用户应该可以无缝地获得体验，而应用程序将通过 *N010* 警告代码，以防它使用AccessEnabler iOS/tvOS SDK。
1. Apple SSO和非Apple SSO身份验证流程之间的MVPD用户ID是否会更改？
   - 预计用户ID不会发生更改，但需要为每个选择的提供商验证该ID。
1. 身份验证TTL是否会有任何更改？
   - Adobe Primetime身份验证将继续遵循程序员集成每个MVPD所需的TTL。
   - 当通过Apple SSO从一个程序员应用程序导航到另一个程序员应用程序时，第二个应用程序将拥有其相应程序员x MVPD集成的TTL（它不会共享验证第一个应用程序的TTL）

|                                      | Adobe Primetime身份验证TTL已过期 | Adobe Primetime身份验证TTL有效 |
| ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| **Apple的设备令牌TTL已过期** | 用户未验证（应显示MVPD选取器） | 用户已完成身份验证，且TTL是其Adobe Primetime身份验证令牌的剩余时间 |
| **Apple的设备令牌TTL有效** | 用户通过静默式身份验证，并使用TVE功能板中指定的TTL获取另一个Adobe Primetime身份验证令牌 | 用户已完成身份验证，且TTL是其Adobe Primetime身份验证令牌的剩余时间 |

<!--

## Resources {#Resources}

- [Apple SSO Cookbook (REST API)](/help/authentication/apple-sso-cookbook-rest-api.md)
- [Apple SSO Cookbook (iOS/tvOS SDK)](/help/authentication/apple-sso-cookbook-iostvos-sdk.md)
- [Sign in with your TV provider on your iPhone, iPad, or iPod touch](https://support.apple.com/en-us/HT207035)
- [Use your pay TV or cable provider with Apple TV](https://support.apple.com/en-us/HT207035)
- [TV providers that let you sign in on your iPhone, iPad, or Apple TV](https://support.apple.com/en-us/HT208084)
- [TV Provider Authentication](https://developer.apple.com/design/human-interface-guidelines/tvos/system-capabilities/tv-provider-authentication/)
- [Apple Developer Documentation - Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount)
-->
