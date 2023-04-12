---
title: Apple SSO概述
description: Apple SSO概述
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1452'
ht-degree: 0%

---



# Apple SSO概述 {#apple-sso-overview}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## 简介 {#Introduction}

Apple提供了一个API，允许用户在设备系统级别登录到其电视提供商帐户，而无需逐个应用程序进行身份验证。

因此，Apple和Adobe Primetime Authentication合作，为iPhone、iPad和Apple电视所有者在TV Everywhere生态系统中创建了单点登录(SSO)平台用户体验。

为了从Apple设备上的单点登录(SSO)用户体验中受益，必须填写先决条件列表。

</br>

## 先决条件 {#Prerequisites}

先决条件可适用于TVE业务中涉及的一个或多个实体，如程序员、MVPD、Adobe Primetime身份验证或Apple。

</br>

### 程序员 {#Programmer}

为了从单点登录(SSO)用户体验中受益，一位程序员必须：

1. 至少使用Xcode版本8和iOS/tvOS版本10。

1. 拥有 [视频订阅者单点登录授权](https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_developer_video-subscriber-single-sign-on) 已配置到其Apple开发人员帐户。 请联系Apple以启用 [视频订阅者帐户框架](https://developer.apple.com/documentation/videosubscriberaccount) 的ID。

1. 通过，为每个所需的集成(Channel x MVPD)和所需平台(iOS / tvOS)启用单点登录(YES) [Adobe Primetime TVE仪表板](https://console.auth.adobe.com/).

1. 使用Apple身份验证团队提供的以下两个解决方案之一集成Adobe Primetime SSO工作流：

   - Adobe Primetime Authentication REST API可以支持在iOS、iPadOS或tvOS上运行的客户端应用程序的最终用户使用平台单点登录(SSO)身份验证。 另请参阅 [Apple SSO指南(REST API)](/help/authentication/apple-sso-cookbook-rest-api.md).

   - Adobe Primetime Authentication AccessEnabler iOS/tvOS SDK可以支持在iOS、iPadOS或tvOS上运行的客户端应用程序的最终用户进行平台单点登录(SSO)身份验证。 另请参阅 [Apple SSO指南(iOS/tvOS SDK)](/help/authentication/apple-sso-cookbook-iostvos-sdk.md).

   - **<u>专业提示：</u>** 为了能够访问用户的订阅信息，用户必须授予应用程序继续操作的权限，这与提供对设备的摄像头或麦克风的访问权限类似。 必须根据应用程序请求此权限，设备将保存用户的选择。 请记住，用户可以通过转到应用程序设置（电视提供商权限访问）或 *`Settings -> TV Provider`* 在iOS/iPadOS或 *`Settings -> Accounts -> TV Provider`* 在tvOS上。

   - **<u>专业提示：</u>** 我们建议在应用程序进入前台状态时请求用户的权限，但这只是建议，因为应用程序可以检查 [访问权限](https://developer.apple.com/documentation/videosubscriberaccount/vsaccountmanager/1949763-checkaccessstatus) 用户在要求用户进行身份验证之前的任意时间点的订阅信息。 此外， AccessEnabler iOS/tvOS SDK API将在需要时自动请求用户的权限。

   - **<u>专业提示：</u>** 我们建议通过解释单点登录(SSO)用户体验的好处，来激励拒绝授予访问订阅信息权限的用户。 请记住，用户可以通过转到应用程序设置（电视提供商权限访问）或 *`Settings -> TV Provider`* 在iOS/iPadOS或 *`Settings -> Accounts -> TV Provider`* 在tvOS上。

结果应该能够根据以下用户流创建一个体验，我们建议您在开始开发应用程序之前先查阅这些体验：

- [iPhone/iPad](http://tve.zendesk.com/hc/article_attachments/205624966/User_flows_AppleSSO_iOS_v2.pdf) 用户流
- [Apple TV](http://tve.zendesk.com/hc/article_attachments/206669126/User_flows_tvOS.pdf) 用户流


>[!IMPORTANT]
>
> 当单点登录功能为 **已启用** (对于iOS/tvOS) **和** 在Apple **已载入（受支持）或选取器** 来自Apple SSO工作流的身份验证/注销流将涉及Apple和Adobe Primetime身份验证解决方案，而所有其他流（授权、预授权、元数据等） 将仅由Adobe Primetime身份验证提供服务。


>[!IMPORTANT]
>
> 当单点登录功能为 **已禁用** (对于iOS/tvOS) **或** 在Apple **未载入（不支持）** 验证/注销流程的MVPD将从Apple SSO工作流回退到仅由Adobe Primetime身份验证服务的常规工作流。


>[!IMPORTANT]
>
> Apple SSO工作流的一个主要优势是单屏幕身份验证用户流，当单点登录功能为 **已启用** 适用于tvOS **和** 在Apple **已载入（支持）** MVPD。


### MVPD {#MVPD}

为了从单点登录(SSO)用户体验中受益，一个MVPD必须：

 

1. 在Apple的一侧，载入Apple SSO工作流。 请联系Apple以促进入门流程。
1. 提供能够处理用户登录表单的JavaScript TVML应用程序。 请联系Apple以获取正确的文档。
1. 提供一个字符串值，该值表示Apple在载入过程中分配的提供程序标识符。 请联系Adobe Primetime身份验证以执行配置更改。

</br>

## 常见问题解答 {#FAQ}

1. 如果Apple SSO工作流出现问题，使用AccessEnabler iOS/tvOS SDK的应用程序是否能够回退到常规身份验证流程？
   - 这是可能的，但需要对 [Adobe Primetime TVE仪表板](https://console.auth.adobe.com/). 的 *启用单点登录* 必须在 *否* (Channel x MVPD)和所需平台(iOS/tvOS)。
   - 应用程序仅在调用后才确认配置更改 [setRequestor](/help/authentication/iostvos-sdk-api-reference.md#setReqV3) API，以防它使用AccessEnabler iOS/tvOS SDK。
1. 应用程序是否知道通过平台SSO在其他设备或其他应用程序上登录后，身份验证何时发生？
   - 此信息将不可用。
1. 应用程序是否知道在同一设备上通过平台SSO登录后，身份验证何时发生？ 
   - 此信息作为用户元数据键的一部分提供： *tokenSource*，应返回字符串值：“Apple”。
1. 如果用户通过转到 *`Settings -> TV Provider`* 在iOS/iPadOS或 *`Settings -> Accounts -> TV Provider`* 在tvOS部分中使用未与应用程序集成的MVPD吗？
   - 用户启动应用程序时，将不会通过Apple SSO工作流对用户进行身份验证。 因此，应用程序必须回退到常规身份验证流程并显示其自己的MVPD选取器。
1. 如果用户通过转到 *`Settings -> TV Provider`* 在iOS/iPadOS或 *`Settings -> Accounts -> TV Provider`* 在tvOS部分中使用具有 *启用单点登录* 设置 *否* 在 [Adobe Primetime TVE仪表板](https://console.auth.adobe.com/) (对于iOS/tvOS平台)?
   - 用户启动应用程序时，将不会通过Apple SSO工作流对用户进行身份验证。 因此，应用程序必须回退到常规身份验证流程并显示其自己的MVPD选取器。
1. 如果用户的MVPD不受Apple载入（不受支持），但Apple选取器中存在MVPD，会发生什么情况？
   - 当用户启动应用程序时，用户将只通过Apple SSO工作流选择MVPD，而无需完成身份验证流程。 因此，应用程序必须回退到常规身份验证流程，但可能使用已选择的MVPD。
1. 如果用户的MVPD不受Apple载入（不支持），会发生什么情况？
   - 当用户启动应用程序时，用户将通过Apple SSO工作流选择“其他电视提供商”选取器选项。 因此，应用程序必须回退到常规身份验证流程并显示其自己的MVPD选取器。
1. 如果用户的MVPD通过媒体降级，会发生什么情况 [Adobe Primetime TVE仪表板](https://console.auth.adobe.com/)?
   - 当用户启动应用程序时，将通过降级机制对用户进行身份验证，而不是通过Apple SSO工作流进行身份验证。
   - 用户的体验应该是无缝的，而应用程序将通过 *N010* 警告代码，以防它使用AccessEnabler iOS/tvOS SDK。
1. Apple SSO和非Apple SSO身份验证流程之间的MVPD用户ID会发生更改吗？
   - 预计用户ID不会更改，但需要为每个选定的提供商验证该用户ID。 
1. 验证TTL是否有任何更改？
   - Adobe Primetime身份验证将继续遵循程序员与每个MVPD集成所需的TTL。
   - 当通过Apple SSO从一个程序员应用程序导航到另一个程序员应用程序时，第二个应用程序将具有其相应程序员的TTL x MVPD集成（它不会共享经验证的第一个应用程序的TTL）

|  | Adobe Primetime身份验证TTL过期 | Adobe Primetime身份验证TTL有效 |
| ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| **Apple设备令牌TTL已过期** | 用户未通过身份验证（应显示MVPD选取器） | 用户已进行身份验证，且TTL是其Adobe Primetime身份验证令牌的剩余时间 |
| **Apple设备令牌TTL有效** | 用户将进行静默身份验证，并获取另一个Adobe Primetime身份验证令牌，该令牌具有TVE功能板中指定的TTL | 用户已进行身份验证，且TTL是其Adobe Primetime身份验证令牌的剩余时间 |

<!--

## Resources {#Resources}

- [Apple SSO Cookbook (REST API)](/help/authentication/apple-sso-cookbook-rest-api.md)
- [Apple SSO Cookbook (iOS/tvOS SDK)](/help/authentication/apple-sso-cookbook-iostvos-sdk.md)
- [Sign in with your TV provider on your iPhone, iPad, or iPod touch](https://support.apple.com/en-us/HT207035)
- [Use your pay TV or cable provider with Apple TV](https://support.apple.com/en-us/HT207035)
- [TV providers that let you sign in on your iPhone, iPad, or Apple TV](https://support.apple.com/en-us/HT208084)
- [TV Provider Authentication](https://developer.apple.com/design/human-interface-guidelines/tvos/system-capabilities/tv-provider-authentication/)
- [Apple Developer Documentation - Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount)
-->
