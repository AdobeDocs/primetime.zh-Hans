---
title: MVPD概述
description: MVPD概述
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2736'
ht-degree: 0%

---


# MVPD概述 {#mvpd-overview}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## 简介 {#intro}

此概述适用于多渠道视频节目分发商(MVPD)。 有关包括Kickstart和集成指南在内的其他文档，请参阅本文档末尾的“相关信息”部分。



随处电视(TVE)是当前著名的行业运动，它使付费电视用户能够跨多个设备访问他们已经付费的内容，包括家庭内和家庭外的内容。  对于付费电视提供商来说，TVE创造了新的机会，既可以保留现有客户关系，也可以启用新客户关系。 然而，随着这些机遇的出现，挑战也随之而来。 在TVE环境中，程序员提供内容，但MVPD保存客户信息，以验证潜在查看者是否是有效订阅者。



与一个程序员协调查看者身份验证和授权可能很简单，但与数十个或数百个不同程序员进行协调变得越来越复杂。 但是，有了Adobe® Pass ,MVPD只需实施单一、简单的集成即可进入整个TVE生态系统，包括NBCUniversal Media 、 Turner Broadcasting(TBS 、 TNT 、 CNN)、Fox Broadcast Networks 、 Hulu等程序员。  Adobe Primetime身份验证提供了一个集成框架，使确定用户权利变得简单和安全。



底线：Adobe Primetime身份验证可安全地介绍程序员和MVPD之间的权利交易，从而方便查看者访问订阅内容。 换句话说，Adobe Primetime身份验证让正确的客户能够轻松、快速地访问正确的内容。


通过Adobe Primetime身份验证，MVPD将收到：

与程序员轻松集成。  通过单个集成，从多个内容所有者提供即时连接。

提高客户参与度。  在客户跨多个平台和设备查看内容时，支持流畅的品牌化体验。

安全身份验证。  确保仅授权用户和设备有权访问优质内容，并（可选）限制每个家庭帐户可以连接的设备和并发流数量。

## 常见问题解答 {#faq}

Adobe Primetime身份验证的安全性如何？ Adobe Primetime身份验证架构的首要任务是确保只有经过授权的查看者才能进行身份验证并授予对高级内容的访问权限。 Adobe Primetime身份验证将访问与观看设备紧密绑定，并有助于限制给定家庭的流、会话和/或设备。


是否需要Flash Player? Adobe Primetime对TV Everywhere的身份验证与播放器和平台无关，可与任何播放应用程序(包括Silverlight和HTML5)集成。 此外，Adobe Primetime身份验证还为运行iOS和Android的手机和平板电脑等设备提供本机支持。


Adobe Primetime身份验证支持哪些设备？ 几乎任何使用HTML5 web kit的设备都支持Adobe Primetime身份验证，以提供浏览器内查看体验。 此外，Adobe Primetime身份验证将继续为各种特定于设备的平台(包括iOS、Android™、Xbox360（已弃用）和AdobeAir®（已弃用）应用程序)推出本机软件开发工具包(SDK)。 最近，Adobe Primetime身份验证为无法呈现浏览器页面的设备（例如，“智能”电视、机顶盒和游戏机）提供了无客户端解决方案。  要使用MVPD验证用户身份，需要能够渲染浏览器页面。


Adobe Primetime身份验证是否支持Tv Everywhere的新兴标准？ Adobe Primetime身份验证符合CableLabs OLCA（在线内容访问）规范，该规范为从在线来源向付费电视客户交付视频提供技术要求和架构。 Adobe于2011年6月参与了CableLabs集成测试项目，并通过了服务提供商实施的测试过程。 Adobe Primetime身份验证已根据OLCA规范进行验证（完整且经过测试）。 授权组件已完成，但测试验证当前正在等待CableLabs测试环境的发布。 Adobe还是OATC（开放认证技术联盟）的积极成员，作为该机构的一部分，参加了几个小组委员会的规范起草项目。



什么是身份验证？ 验证是MVPD确认给定用户是已知客户的过程。



什么是授权？ 授权是MVPD确认经过验证的用户对给定资源有效订阅的过程。



## 架构 {#architecture}

Adobe Primetime身份验证是一种托管服务，它允许根据MVPD和程序员所需的业务规则进行快速后端（服务器到服务器）集成。 这意味着为所有各方快速上市、提供更安全的防欺诈环境，并提供出众的客户体验，让更多的电视内容可以跨更多平台提供给更多的人。


Adobe Primetime身份验证通过软件即服务(SaaS)模式提供，并使最终用户、MVPD和程序员之间能够进行更加安全的通信，以验证对内容的授权。 该服务的核心组件包括：

服务器端 — 托管的Adobe Primetime身份验证服务器。 这是一个应用服务器，它与MVPD的验证系统进行后通道（服务器到服务器）通信。
客户端：客户端Access Enabler - Access Enabler是一个小文件，加载到程序员的网页或播放器应用程序中。 它为程序员的内容查看应用程序提供授权API，并与Adobe Primetime身份验证服务器通信。
无客户端Web服务（适用于非Web功能设备） — RESTful Web服务，为智能电视、游戏机和机顶盒等设备提供授权API。

>[!NOTE]
>
>作为MVPD，您的Web服务必须能够识别来自Adobe Primetime身份验证的身份验证和授权请求，并以预期格式响应所需数据。

Adobe Primetime身份验证允许您为客户提供联合身份管理，也称为单点登录(SSO)身份验证和授权。 使用Adobe Primetime身份验证后，只要MVPD允许该身份验证保持不变，订阅者就无需在首次身份验证后再次登录。 （通常为30天。） 为实现此目的，Adobe Primetime身份验证为我们的客户提供了一个用于身份验证令牌的通用域。 此身份验证状态信息适用于与给定MVPD集成的所有参与站点。


目前，与MVPD的大多数Adobe Primetime身份验证集成都使用SAML协议，SAML协议是主要身份验证标准之一。 Adobe Primetime身份验证在SAML架构中充当代理服务提供程序，并在Adobe公共域中将SAML身份验证响应作为安全令牌保留。 Adobe Primetime身份验证符合SAML 2.0。 但是，尽管Adobe Primetime身份验证目前通常与SAML SSO解决方案一起使用，但Adobe Primetime身份验证架构未绑定到任何特定协议。 因此，可以随着时间的推移添加对新协议（例如基于OAuth 2.0或自定义协议的协议）的支持。


Adobe可与MVPD的技术团队合作配置Adobe Primetime身份验证，以满足任何现有集成的需求。 MVPD的集成是免费的，前提是采用“标准”集成并且满足最低的支持要求（文档和基本电子邮件支持）。 如果MVPD需要大量支持或时间表上升，则可能需要支付支持费用，或者提供商可能希望与熟悉我们解决方案（如Syncor）的第三方合作。


Adobe Primetime身份验证还支持有效处理MVPD业务逻辑，如下所示：

对于自包含的业务逻辑，当收到授权请求时，MVPD可以应用该业务逻辑，当MVPD收到授权请求时，Adobe会提供支持业务逻辑执行所需的必要数据。 此数据可以包括（但不限于）发出请求的用户的唯一设备ID和设备的IP地址。

对于需要用户干预和/或由Adobe解决方案进行特定处理的业务逻辑，Adobe可以为每个MVPD维护一些自定义属性。 这些特定于MVPD的配置/策略包括启用预定义的工作流，这些工作流可在顶级工作流的特定时间点启动。 有关自定义资产支持的详细信息，请联系您的Adobe代表。

下图说明了MVPD和程序员与这些Adobe Primetime身份验证组件的关系：

![](assets/high-level-architecture-nflows.png)

*图：高级架构和流*

## Adobe Primetime身份验证组件 {#components}

下面概述了Adobe Primetime身份验证生态系统的一些主要组件。 这些功能包括：

* [Access Enabler / Clientless Web服务](#ae)
* [Adobe托管的后端服务器](#backend)
* [令牌](#tokens)

### 访问启用程序/无客户端Web服务 {#ae}

Access Enabler方便了与用户进行的所有身份验证和授权交互，并在其系统本地运行。 Access Enabler通过MVPD处理实际的授权工作流，而程序员则负责更高级别的网页或播放器应用程序。

无客户端Web服务由Adobe Primetime身份验证为无法呈现网页的设备提供。  对于这些设备，授权过程会在智能设备上启动并查看内容，而使用MVPD的身份验证则在支持Web的设备（PC、智能手机和平板电脑）上进行。

Access Enabler（访问启用程序）：

* 启动特定于MVPD的身份验证和授权工作流。
* 缓存每个程序员资源/渠道的成功授权响应以最大限度地减少不必要的请求流量。
* 可以为特定于每个MVPD的预定义工作流进行配置，如显式设备注册。
* 它在以下表单中可用：
   * Flash Player运行时可以执行的SWF文件
   * 浏览器直接执行的JS文件
   * 适用于各种平台(包括iOS、Android和Xbox)的本机Access Enabler。

### Adobe托管的后端服务器 {#backend}

由Adobe托管的Adobe Primetime身份验证后端服务器：

* 使用需要Adobe Primetime身份验证与运营商之间服务器到服务器通信的MVPD设置身份验证和授权工作流。
* 维护程序员站点和应用程序的配置。
* 托管可下载的Access Enabler组件文件。
* 生成身份验证和授权令牌。

### 令牌 {#tokens}

Adobe Primetime身份验证授权解决方案的核心是生成在成功完成身份验证/授权工作流程后获得的特定数据段。 这些数据称为令牌。 它们的有效期有限，并且安全地存储在依赖于平台的位置。 到期后，必须通过重新启动身份验证和/或授权工作流来重新发布令牌。

在身份验证/授权工作流程中发布了三种类型的令牌。 两个是“长期存在”的，它们为用户的观看体验提供了连续性。 第三种是短暂的令牌，它支持通过流跳转来减轻欺诈的行业最佳实践。 令牌的生存时间(“TTL”)值根据MVPD与程序员之间的协议进行设置。 您可以决定最适合您的业务和客户的TTL值。

**长期使用的身份验证令牌**. 客户使用Adobe Primetime身份验证成功登录其MVPD帐户后，即会进行身份验证成功。 然后，Adobe Primetime身份验证会生成与请求设备绑定的长期身份验证(“authN”)令牌，并且（取决于MVPD）会生成匿名标识用户的全局唯一标识符(“GUID”)。

**长期使用的授权令牌**. 成功授权后，Adobe Primetime身份验证会创建一个长期授权(“authZ”)令牌。 此令牌不可移植，因为它与请求设备和特定的受保护资源（例如渠道、系列或剧集）绑定。 Access Enabler使用长寿命的authZ令牌创建用于实际查看访问的短寿命媒体令牌。

**短暂的媒体令牌**. 用户获得授权后，Adobe Primetime身份验证会生成authZ令牌，并使用该令牌生成由Adobe签名并加密的一次性、短期的媒体令牌，以避免在交换期间发生篡改。 由于短期令牌通过访问启用程序API或无客户端Web服务公开到嵌入站点，因此在提供对受保护资源的访问之前，程序员的媒体服务器必须使用Adobe Primetime身份验证组件（媒体令牌验证器）来验证令牌。

## MVPD集成生命周期 {#lifecycle}

下图显示了Adobe Primetime身份验证与MVPD之间集成的生命周期。

![](assets/mvpd-int-lifecycle.png)

*图：MVPD集成生命周期*

## 权利流程图 {#chart}

以下流程图介绍了使用Adobe Primetime身份验证确认权利的整个过程：

![](assets/authn-authz-entitlmnt-flow.png)

*图：使用Adobe Primetime身份验证确认权利的过程*

## 身份验证步骤 {#authn-steps}

以下步骤演示了Adobe Primetime身份验证流程的示例。  这是授权流程的一部分，程序员在该流程中确定用户是否是MVPD的有效客户。  在此方案中，用户是MVPD的有效订阅者。  用户正在尝试使用程序员的Flash应用程序查看受保护的内容：

1. 用户浏览到程序员网页，该网页将程序员的Flash应用程序和Adobe Primetime身份验证访问启用程序组件加载到用户的计算机上。 Flash应用程序使用Access Enabler通过Adobe Primetime身份验证来设置程序员的标识，而Adobe Primetime身份验证将Access Enabler作为程序员的配置和状态数据的前缀（“请求者”）。 在执行任何其他API调用之前，Access Enabler必须从服务器接收此数据。  技术说明：程序员使用Access Enabler&#39;s `setRequestor()` 方法；有关详细信息，请参阅 [程序员集成指南](/help/authentication/programmer-integration-guide-overview.md).
1. 当用户尝试查看程序员的受保护内容时，程序员的应用程序向用户显示MVPD列表，用户从中选择提供商。
1. 用户将被重定向到Adobe Primetime身份验证服务器，该服务器会为用户选择的MVPD创建加密的SAML请求。 此请求将作为代表程序员向MVPD发送的身份验证请求。 根据MVPD的系统，用户的浏览器随后会被重定向到MVPD的站点以登录，或者在程序员的应用程序中创建登录iFrame。
1. 无论是在哪种情况下（重定向还是iFrame），MVPD都会接受请求并显示其登录页面。
1. 用户使用MVPD登录，MVPD将验证用户作为付费客户的状态，然后MVPD创建自己的HTTP会话。
1. 验证用户后，MVPD会创建一个响应（SAML和加密），MVPD会将该响应发送回Adobe Primetime身份验证。
1. Adobe Primetime身份验证接收MVPD响应，发现有一个Adobe Primetime身份验证HTTP会话打开，验证 [SAML](https://en.wikipedia.org/wiki/Security_Assertion_Markup_Language) 来自MVPD的响应，并重定向回程序员网站。
1. 重新加载程序员站点，重新加载Access Enabler，程序员再次调用setRequestor()。  对setRequestor()的第二次调用是必需的，因为当前配置已更改 — 现在存在一个标记，该标记通知Access Enabler AuthN令牌正在等待在服务器上生成。
1. Access Enabler会发现有待处理的身份验证，并从Adobe Primetime身份验证服务器请求令牌。 通过调用Flash Player的DRM功能，可从服务器中检索令牌。
1. AuthN令牌存储在程序员的Flash PlayerLSO缓存中；身份验证现已完成，会话在Adobe Primetime身份验证服务器上被销毁。

## 授权步骤 {#authz-steps}

从上一节([身份验证步骤](#authn-steps)):

1. 当用户尝试访问程序员保护的内容时，程序员的应用程序首先在用户的本地计算机或设备上检查AuthN令牌。  如果令牌不在，则 [身份验证步骤](#authn-steps) 之后是。  如果AuthN令牌存在，则授权流程将随程序员应用程序发起对Access Enabler的调用而进行，该调用请求获取用户对受保护内容特定项目的查看权限。
1. 受保护内容的特定项目由“资源标识符”表示。  这可以是一个简单的字符串或更复杂的结构，但无论如何，资源标识符的性质是在程序员和MVPD之间提前商定的。  程序员的应用程序将资源标识符传递给Access Enabler。  Access Enabler在用户的本地计算机或设备上检查AuthZ令牌。  如果AuthZ令牌不在，则Access Enabler会将请求传递到后端Adobe Primetime身份验证服务器。
1. Adobe Primetime身份验证服务器使用标准化协议与MVPD授权端点通信。  如果MVPD响应指示用户有权查看受保护的内容，则Adobe Primetime身份验证服务器将创建一个AuthZ令牌，并将其传递回Access Enabler，Access Enabler将AuthZ令牌存储在用户计算机上。
1. 通过将AuthZ令牌存储在用户的机器或设备上，程序员的应用程序调用Access Enabler以从Adobe Primetime身份验证服务器获取媒体令牌，并将该令牌提供给程序员的应用程序。
1. 最后，程序员的应用程序使用媒体令牌验证器组件来确认正确的用户正在查看正确的内容，并且在媒体令牌就位后，允许用户查看受保护的内容。

<!--
>![RELATEDINFORMATION]
>
>*   Kickstart Guides, [MVPD kickstart](/help/authentication/mvpd-kickstart-guide.md) and [programmer kickstart](/help/authentication/programmer-kickstart-guide.md). These guides explain the initial steps to take to begin integrating with Adobe Primetime authentication.
>
>*   [MVPD Integration Guide](/help/authentication/mvpd-kickstart-guide.md). This is a lower level technical guide for MVPDs, directed primarily to the software engineers who code and test the applications and systems involved in the integration.
>
>*   [Overview For Programmers](/help/authentication/programmer-overview.md). The same high level of conceptual information as in this MVPD overview, but directed toward the content providers (Programmers).
-->
