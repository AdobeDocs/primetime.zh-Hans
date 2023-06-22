---
title: 面向程序员的概述
description: 面向程序员的概述
exl-id: 64a12e49-0ecb-4b81-977d-60c10925bb59
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '4272'
ht-degree: 0%

---

# 面向程序员的概述 {#programmers-overview}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权的使用。

## 介绍 {#introduction}

本概述适用于计划将Adobe®传递至其网站或应用程序的内容提供商（程序员）。 有关其他文档（包括Kickstart和集成指南），请参阅下面的相关信息。

如今，您的查看者可以随时随地上网，并直接向程序员请求访问受保护的内容。 他们可能希望观看一次性活动，或者可能希望获得您正在播放的整个电视剧的观看权。

但在您允许访问受保护的内容之前，您必须确定客户是否有资格查看该内容。 他们是否订阅了多频道视频节目分发商(MVPD)？ 如果是，该订阅是否包含您的编程？

对于程序员来说，确定查看者的权利并不总是简单的。 MVPD拥有其客户的标识数据和访问权限。  此外，查看者尝试访问您的受保护内容时，会订阅各种MVPD，而每种MVPD都有不同的系统，这一事实很容易说明，确定查看者是否有权访问受保护内容会迅速变得复杂且具有技术挑战性：

![](assets/user-ent-by-progr.png)

*图：由程序员直接确定的用户权利*

TV Everywhere的Adobe Primetime身份验证安全地协调程序员和MVPD之间的授权事务。 Adobe Primetime身份验证使程序员可以轻松、快速、安全地向有效客户提供受保护的内容：

![](assets/user-ent-mediatedby-authn.png)

*图：由Adobe Primetime身份验证调解的用户权利*

Adobe Primetime身份验证充当您与参与MVPD进行交换的代理，因此您可以使用一致的跨站点界面来呈现查看器。 Adobe Primetime身份验证还允许您为查看器提供单点登录(SSO)身份验证和授权。 对所有参与的服务进行身份验证和授权跟踪，这样用户就无需在自己的系统上首次身份验证后再次登录。

* **身份验证**  — 向MVPD确认给定用户是已知客户的过程。
* **授权**  — 向MVPD确认经过身份验证的用户对指定资源具有有效订阅的过程。

### Adobe Primetime身份验证的工作原理 {#HowItWorks}

程序员的内容查看应用程序使用Access Enabler客户端组件或无客户端API的RESTful Web服务（适用于智能电视、游戏机、机顶盒等不支持Web的设备）与Adobe Primetime身份验证交互。 Access Enabler在用户系统上运行，它有助于执行所有权利工作流。  当客户访问您的网站并请求受保护的内容时，将Adobe从其托管网站下载Access Enabler组件。  Adobe Primetime身份验证服务器托管无客户端解决方案中使用的RESTful Web服务。

Adobe Primetime身份验证处理实际的权利工作流，同时提供用于以下目的的原始项：

* 设置您的身份。 (程序员是Adobe Primetime身份验证权利流程中的“请求者”。)
* 使用特定MVPD验证用户。  (MVPD是Adobe Primetime身份验证权利流中的“身份提供程序”或“IdP”。)
* 使用MVPD授权用户访问特定资源。
* 注销用户。

程序员负责执行以下操作的上层网页或播放器应用程序：

* 实施用户界面
* 与Access Enabler或无客户端API Web服务交互

Adobe Primetime身份验证的目标是为程序员和MVPD创建一种简单的模块化方式来处理授权验证。

## 了解令牌 {#understanding-tokens}

Adobe Primetime身份验证权利解决方案侧重于生成在身份验证和授权工作流成功完成时创建的特定数据段。 这些数据段称为令牌。 令牌的生命周期有限；当其过期时，需要通过重新启动身份验证和授权工作流重新颁发令牌。

有关令牌的详细信息，请参阅以下部分：

* [令牌类型](#token-types)
* [令牌存储](#token-storage)
* [令牌安全](#token-security)
* [令牌共享](#token-sharing)

### 令牌类型 {#token-types}

在身份验证和授权工作流期间会颁发三种类型的令牌。 AuthN和AuthZ令牌是“长效的”，为用户的观看体验提供了连续性。 媒体令牌是一个短暂的令牌，它支持行业最佳实践，以防止通过流翻录进行欺诈。 程序员根据与MVPD达成的协议为每种类型的令牌指定生存时间(TTL)值。 程序员决定最适合您的企业和客户的TTL价值。

* **身份验证令牌** （“长期”）：在成功进行身份验证后，Adobe Primetime身份验证将创建一个与请求设备和全局唯一标识符(GUID)都关联的AuthN令牌。
   * Adobe Primetime身份验证将AuthN令牌发送到Access Enabler，后者会在客户端系统上安全地缓存该令牌。  当AuthN令牌存在且未过期时，它可供所有使用Adobe Primetime身份验证的应用程序使用。 Access Enabler将AuthN令牌用于授权流。
   * 在任何给定时刻，仅缓存一个AuthN令牌。 每当颁发了新的AuthN令牌并且旧令牌已存在时，Adobe Primetime身份验证就会覆盖缓存的令牌。
* **AuthZ令牌** （“长期”）：在成功授权后，Adobe Primetime身份验证会创建一个与请求设备和特定的受保护资源关联的AuthZ令牌。  受保护的资源由唯一的资源ID标识。
   * Adobe Primetime身份验证将AuthZ令牌发送到Access Enabler，后者会在本地系统上安全地缓存该令牌。 然后，Access Enabler使用AuthZ令牌创建用于实际查看访问的短暂媒体令牌。
   * 在任何给定时间，每个资源仅缓存一个AuthZ令牌。 Adobe Primetime身份验证可以缓存多个AuthZ令牌，前提是这些令牌与其他资源关联。 每当颁发了新的AuthZ令牌并且同一资源已存在旧令牌时，Adobe Primetime身份验证就会覆盖缓存的令牌。
* **媒体令牌** （“短期”）：Access Enabler使用AuthZ令牌生成短期（默认值： 7分钟）媒体令牌。 这时，即认为播放请求已成功。
   * 在提供对受保护资源的访问权限之前，您的媒体服务器必须使用Adobe Primetime身份验证组件（媒体令牌验证器）来验证媒体令牌。
   * 由于媒体令牌未绑定到设备，因此其生命周期明显短于长期AuthN和AuthZ令牌（默认值： 7分钟）。
   * 短暂的媒体令牌限制为一次性使用，并且从不缓存。 每次调用授权API时，都会从Adobe Primetime身份验证服务器检索它。

### 令牌存储 {#token-storage}

Access Enabler将长期令牌（AuthN和AuthZ）存储在特定于其环境的位置：

* **Flash10.1** （或更高版本）：长生命周期令牌存储为本地共享对象。
* **HTML5**：长效令牌安全地保存在HTML5浏览器的本地存储中。
* **iOS**：长效令牌存储在永久性粘贴板上，其他Adobe Primetime身份验证客户端应用程序可以访问该令牌。
* **Android**：长效令牌存储在共享数据库文件中，其他Adobe Primetime身份验证客户端应用程序可以在该文件中访问它们。
* **无客户端API设备**：令牌存储在Primetime身份验证服务器上。

### 令牌安全 {#token-security}

Adobe Primetime身份验证服务器使用设备ID（派生自设备的硬件特征）对所有长期令牌进行数字签名。 数字签名的生成、保护和验证方式因环境而异：

* **Flash10.1** （或更高版本） — 设备ID依赖于设备凭据，该凭据是从Adobe个性化服务器颁发的唯一证书。 此安全性相当于FAXS DRM技术。 此服务器端验证会将令牌中的唯一设备ID与设备凭据(在Flash Player与Adobe Primetime身份验证之间安全通信)进行比较。 设备凭据还标识了FAXS客户端版本以及向其发出凭据的Flash Player(或AIR)版本。 设备绑定比设备绑定更强，因此HTML的令牌生存时间(TTL)通常比Flash更长。
* **HTML5**  — 设备在客户端个性化。 它使用JavaScript提供的特征来生成包括浏览器和操作系统版本的伪设备ID、IP地址和浏览器Cookie GUID（全局唯一标识符）。 此令牌设备ID将与设备的当前伪设备ID进行比较。 由于IP地址在正常使用期间可能会更改，因此即使在同一个会话中，Adobe Primetime身份验证也会将HTML5令牌存储在两个位置：localStorage和sessionStorage。 如果IP发生更改且sessionStorage令牌在其他情况下仍然有效，则会维护会话。 对于HTML5，设备绑定没有那么强，因此令牌的TTL通常比Flash的短。
* **本机客户端** (iOS和Android) — 长效令牌包含本机设备ID个性化信息，因此将绑定到请求设备。 身份验证和授权请求通过HTTPS发送，设备ID信息在发送到后端服务器之前由Access Enabler库进行数字签名。 在服务器端，设备ID信息将根据其关联的数字签名进行验证。
* **无客户端API客户端**  — 无客户端API解决方案具有一组涉及对所有API调用进行数字签名的安全协议。 权利流期间生成的令牌安全地存储在Adobe Primetime身份验证服务器上。

Adobe Primetime身份验证将验证每个长效令牌，以确保访问内容的设备与颁发令牌的设备相同。 对于所有令牌，客户端验证可确保数字签名保持不变，并保留令牌的完整性。 当设备ID验证失败时，身份验证会话将失效，并提示用户再次登录，这将重置令牌。

### 令牌共享 {#token-sharing}

不同平台上的应用程序不共享令牌。 这种情况有很多原因，其中包括：

* 如中所述 [令牌存储](#token-storage)，令牌的存储方法因平台而异(例如，用于Flash的本地共享对象、用于JavaScript的WebStorage )。
* 不同平台之间的令牌安全程度不同。 例如，使用FAXS将Flash令牌强绑定到设备。 纯JavaScript环境中的令牌没有与Flash中相同级别的DRM支持。  与Flash应用程序共享JS令牌会增加安全级别较低的令牌利用更安全环境的可能性。

## 程序员集成生命周期 {#prog-integ-lifecycle}

![](assets/progr-flow-int-lifecycle.png)

*图：将身份验证与程序员的网站和应用程序集成*


## 逻辑流 {#logical-flows}

### 权利流程图 {#chart}

以下流程图显示了确认权利的整体过程(使用Adobe Primetime Authentication Access Enabler客户端组件)：

![](assets/ent-flowchart.png)

*图：确认权利的过程*

### 身份验证步骤 {#authn-steps}

以下步骤显示了Adobe Primetime身份验证流程的示例。  这是授权过程的一部分，在该过程中，程序员确定用户是否为MVPD的有效客户。  在此方案中，用户是MVPD的有效订阅者。  用户正在尝试使用程序员的Flash应用程序查看受保护的内容：

1. 用户浏览到程序员的网页，该网页将程序员的Flash应用程序和Adobe Primetime身份验证访问启用程序组件加载到用户的计算机上。 Flash应用程序使用Access Enabler设置程序员的身份与Adobe Primetime身份验证，而Adobe Primetime身份验证为该程序员（“请求者”）的配置和状态数据设置Access Enabler。 在执行任何其他API调用之前，Access Enabler必须从服务器接收此数据。 技术说明：程序员使用Access Enabler的 `setRequestor()` 方法；有关详细信息，请参见 [程序员集成指南](/help/authentication/programmer-integration-guide-overview.md).
1. 当用户尝试查看程序员的受保护内容时，程序员的应用程序向用户显示MVPD列表，用户从中选择提供程序。
1. 用户将被重定向到Adobe Primetime身份验证服务器，其中已加密 [SAML](https://en.wikipedia.org/wiki/Security_Assertion_Markup_Language) 将创建用户选定MVPD的请求。 此请求作为代表程序员的身份验证请求发送到MVPD。 根据MVPD的系统，随后用户的浏览器将被重定向到MVPD的站点以登录，或者在程序员的应用程序中创建一个登录iFrame。
1. 无论是哪种情况（重定向还是iFrame），MVPD都会接受请求并显示其登录页面。
1. 用户通过MVPD登录，MVPD验证用户作为付费客户的状态，然后MVPD创建自己的HTTP会话。
1. 验证用户后，MVPD会创建一个响应（SAML和加密），然后MVPD会将该响应发送回Adobe Primetime身份验证。
1. Adobe Primetime身份验证接收MVPD响应，看到Adobe Primetime身份验证HTTP会话已打开，验证来自MVPD的SAML响应，并重新导向回程序员网站。
1. 重新加载程序员网站，重新加载Access Enabler，然后程序员再次调用setRequestor()。  需要第二次调用setRequestor()，因为当前配置已更改 — 现在存在一个标志，用于通知Access Enabler等待在服务器上生成AuthN令牌。
1. Access Enabler发现一个挂起的身份验证，并向Adobe Primetime身份验证服务器请求令牌。 通过调用Flash Player的DRM功能，从服务器检索令牌。
1. AuthN令牌存储在程序员的Flash PlayerLSO缓存中；身份验证现已完成，并且会话在Adobe Primetime身份验证服务器上被破坏。

### 授权步骤 {#authz-steps}

以下步骤继续从 [身份验证步骤](#authn-steps)：

1. 当用户尝试访问程序员的受保护内容时，程序员的应用程序首先会检查用户的本地计算机或设备上是否存在AuthN令牌。  如果令牌不存在，则 [身份验证步骤](#authn-steps) 以上步骤如下所示。  如果存在AuthN令牌，则授权流程继续进行，程序员应用程序启动对Access Enabler的调用，请求获取用户对受保护内容的特定项目的查看权限。
1. 受保护内容的特定项目由“资源标识符”表示。  这可以是一个简单的字符串或更复杂的结构，但在任何情况下，资源标识符的性质在程序员和MVPD之间提前商定。  程序员的应用程序将资源标识符传递给Access Enabler。  Access Enabler检查用户的本地计算机或设备上是否存在AuthZ令牌。  如果AuthZ令牌不存在，则Access Enabler将请求传递到后端Adobe Primetime身份验证服务器。
1. Adobe Primetime身份验证服务器使用标准化协议与MVPDs授权端点通信。  如果MVPD的响应表明用户有权查看受保护的内容，则Adobe Primetime身份验证服务器会创建一个AuthZ令牌，并将其传递回Access Enabler，后者将AuthZ令牌存储在用户的计算机上。
1. 当用户计算机或设备上存储有AuthZ令牌时，程序员的应用程序会调用Access Enabler以从Adobe Primetime身份验证服务器获取媒体令牌，并将该令牌提供给程序员的应用程序。
1. 最后，程序员的应用程序使用媒体令牌验证器组件来确认正确的用户正在查看正确的内容，并且在媒体令牌到位后，允许用户查看受保护的内容。


## 注册和初始化 {#reg-and-init}

使用Adobe Primetime身份验证的第一步是向Adobe或Adobe Primetime身份验证授权的合作伙伴注册。

注册时，您将提供与Adobe Primetime身份验证进行通信所基于的域的列表。 例如，Turner Broadcasting System域包括tbs.com和tnt.tv，作为Adobe Primetime身份验证注册的域。 这些内容站点中的每一个站点都有权访问Adobe Primetime身份验证，并分配有自己的请求者ID（例如，“TBS”和“TNT”）。 如果您决定添加其他站点，则必须通知Adobe其他域名，以便将其添加到允许的域列表中，并为其提供其他请求者ID。

>[!WARNING]
>
>测试集成时，请确保测试服务器位于您打算在生产中使用的注册域上。 来自未列入白名单的域的请求（甚至测试请求）将被忽略。 例如，如果您请求在生产中使用domain.com ，请确保将测试集成部署在domain.com、test.domain.com和staging.domain.com下。
>
>即使已将域列入白名单，也会忽略URL中包含用户名和/或密码的请求。 示例： `//username@registered-domain/`

在与Adobe Primetime身份验证的Access Enabler客户端组件进行的所有通信中，请求者ID唯一标识程序员的客户端。 与程序员关联的所有Adobe Primetime身份验证静态数据都使用此ID作为键值。

>[!TIP]
>
>除了您的请求者ID之外，在注册时，您还会收到Access Enabler客户端组件和媒体令牌验证器的功能URL。

## 集成步骤 {#integration-steps}

>[!TIP]
>
>如果您在媒体播放器开发中使用AdobeOpen Source Media Framework(“OSMF”)，则使用Adobe Primetime身份验证的最快方法是集成OSMF插件 *（已弃用）* 到你的玩家代码中。
>
><!--For details, see [Adobe Primetime authentication Plugin For OSMF](https://tve.helpdocsonline.com/9-2-2) in the Programmer Integration Guide.-->

1. [请求者设置](#requestor)
1. [处理身份验证和授权](#authn-authz)
1. [支持单一注销](#ssl)

### 1.申请人设置 {#requestor}

#### 1a. 向Adobe注册

您的第一步是注册Adobe或Adobe Primetime身份验证授权合作伙伴。  注册后，您将获得一个或多个全局唯一标识符(GUID)。 您颁发的每个GUID都与允许从中访问Adobe Primetime身份验证的域相关联。 您可以为请求域传递一个GUID（称为请求者ID），以便为与Access Enabler交互的每个会话注册您的身份。 有关详细信息，请参阅 [注册和初始化](#reg-and-init) 在程序员集成指南中。

#### 1b. Initial Access Enabler集成

下一步是将访问启用程序集成到您现有的媒体播放器应用程序或网页中：

* 您可以嵌入Flash版本， `AccessEnabler.swf`Flash ，或者，您可以将其直接嵌入网页的HTML中。 您可以使用ActionScript或JavaScript与Access EnablerSWF通信。 基本APIActionScript，但是，如果您希望使用JavaScript，可以在页面上包含完整的包装库。
* 对于非Flash环境，您可以：
   * 使用HTML5/JavaScript版本AccessEnabler.js，并通过JavaScript API与其通信
   * 使用适用于Adobe Primetime身份验证的AIR本机扩展将本机代码与内置的ActionScript类相结合
   * 使用Access Enabler库的其中一个本机客户端版本(iOS或Android)

### 2.处理身份验证和授权 {#authn-authz}

#### 2a. 与Access Enabler通信

Access Enabler与网页或播放器应用程序之间的通信是异步的。 您的应用程序调用Access Enabler方法，Access Enabler通过回调进行响应，回调是您在Access Enabler库中注册的。

* 当您的应用程序发出授权请求时，如果本地系统上尚不存在有效的AuthN令牌，则Access Enabler会自动启动身份验证请求。 身份验证成功后，用户的AuthN令牌将存储在本地，因此他们不需要再次登录。 如果他们在任何其他上下文中通过Adobe Primetime身份验证成功进行了身份验证（例如，通过MVPD网站或使用其他程序员），则Access Enabler可以访问本地AuthN令牌，而无需其他身份验证。
* 当用户尝试访问您的受保护内容时，您向Access Enabler发送授权请求。 验证（或启动）身份验证后，Access Enabler联系MVPD(通过Adobe Primetime身份验证服务器)，以确定客户是否有权查看受保护的内容。 您的应用程序只需要将请求发送到Access Enabler，然后处理响应（授权成功或失败）。 如果授权成功，则在客户端系统上存储AuthZ令牌。  最后，您的应用程序会收到一个短暂的媒体令牌，以便在您自己的授权过程中使用。

>[!NOTE]
>
>* 身份验证作为SAML交换，在作为服务提供商(SP)的Adobe Primetime身份验证和作为身份提供程序(IdP)的MVPD之间发生。
>
>* 授权在Adobe Primetime身份验证(SP)和MVPD(IdP)之间使用后端渠道（服务器到服务器）Web服务交换。



#### 2b. 提供授权用户界面 {#entitlement-ui}

您提供自己的UI以便用户访问您的内容。 某些元素（例如实际登录过程）由MVPD提供，而某些元素可以选择作为Adobe Primetime身份验证的一部分提供。 您至少应执行以下操作：

* **实施一个MVPD选择接口，该接口允许新用户识别其MVPD并首次登录**. 对于开发， Access Enabler提供了一个基本的用户界面，使客户能够选择MVPD并启动登录过程。 对于生产，您必须实施自己的MVPD选择器对话框。 有些MVPD会重定向到自己的站点进行登录，而有些则要求在iFrame中显示其登录页面。 您必须实施创建此iFrame的回调以处理用户的MVPD在iFrame中显示其登录页的情况。
* **识别受保护的内容**. 受保护的内容需要授权才能访问。 您的界面应指示哪些内容受到保护，以及哪些内容已获得授权。  授权状态通常以“已解锁”和“已锁定”图标表示。
* **显示用户已通过身份验证**. 您应该将用户的身份验证状态指示为您用于识别受保护内容的任何方法的一部分。 您可以查询Access Enabler以确定客户是否已通过身份验证。

#### 2c. 集成媒体令牌验证器 {#int-media-token-ver}

必须将Adobe Primetime身份验证媒体令牌验证器组件集成到媒体服务器中。  这样，您现有的令牌验证器就能通过成功的授权识别从Adobe Primetime身份验证提供的短暂媒体令牌。 在您向用户提供对受保护内容的访问权限之前，媒体令牌验证器会对媒体令牌进行验证作为最后的安全步骤。 向Adobe注册时，您将收到下载媒体令牌验证器的位置。

### 3.支持单一注销 {#ssl}

在大多数情况下，您的媒体播放器负责通过简单的Access Enabler API处理用户注销。 调用logout()时，Access Enabler执行以下操作：

* 注销当前用户
* 清除已注销用户的所有身份验证和授权信息
* 从用户的本地系统中删除所有AuthN和AuthZ令牌

如果用户让其计算机空闲足够长的时间以使令牌过期，则用户仍然可以返回到会话并成功启动注销。 Adobe Primetime身份验证可确保删除所有令牌，并通知MVPD删除其会话。

从未与Adobe Primetime身份验证集成的站点启动注销时，MVPD可以通过浏览器重定向调用Adobe Primetime身份验证单次注销服务。

## 了解用户ID {#user-ids}

从概念上讲，启动权利流的每个用户都与一个唯一的用户ID相关联。  但是，在权利流的过程中，该用户ID可能会以不同的方式显示，具体取决于您从哪个API获取该ID。

短媒体令牌中的sessionGUID是UserID的安全形式，可通过sendTrackingData()调用使用。   在所有当前集成中，这是用户在不同时间和设备上的永久GUID，但GUID的源在来自MVPD的SAML响应中以用户ID开头。   但是，一些MVPD可能会在未来改变主意，并开始发送临时GUID。  如果程序员希望确保AuthN响应中的MVPD源用户ID是永久性的，他们应在与MVPD签订的协议中对此进行安排。

以下是在Adobe Primetime身份验证API中表示用户ID的不同方式：

* `sendTrackingData()` GUID属性 — 这是MVPD UserID的Adobe哈希版本。  此用户ID经过哈希处理，因此不能从MVPD跟踪回源。   此ID是唯一的，且通常具有持久性，但无法与MVPD共享，因此无法将特定使用行为与MVPD一侧具有的行为进行比较。   它没有数字签名，因此对于防欺诈而言并非不可欺骗，但对于分析来说却足够好。  此形式的用户ID是在Adobe Primetime身份验证在AuthN/AuthZ流中生成的所有事件的客户端提供的。
* 短媒体令牌 `sessionGUID` 属性 — 这与通过访问的UserID相同。 `sendTrackingData()`但是，此服务器进行了数字签名以保护其完整性。  这使得该值足以用于并发使用情况的欺诈跟踪。 此视频流将在使用我们的验证器库后在服务器端进行处理，并可在将视频流释放给客户端之前对欺诈模式进行分析。  这些任务中的任何一个都由程序员来完成。
* `getMetadata() userID `property — 此属性将允许Adobe向程序员公开实际的源MVPD UserID。 它将使用我们从程序员那里获得的证书中的公钥进行加密，因此它不会以明文形式向客户端公开。 这会为程序员提供来自MVPD的实际UserID，因此它可用于直接与MVPD进行帐户关联或欺诈调查。

**总结**

* MVPD用户ID通常是永久性唯一ID，但不保证是 **从MVPD生成，并在成功验证时传递给Adobe**. 除一些例外情况外，所有网络通常都是一致的。
* MVPD用户ID不包含PII，它不是帐号。 它不需要以加密形式公开，因为我们已通过所有MVPD验证未发送任何PII。


用户ID的使用方式取决于用例：

* 如果您需要它来进行跟踪/分析，最实用的方法就是从获取 `sendTrackingData()`.
* 如果在服务器端需要用于流发布、欺诈或操作数据，则可以从“媒体令牌验证器”中获取它。
* 如果您需要它来关联帐户和进行更深入的欺诈，请与您的Adobe联系人联系以获取可用性。

<!--
>[!RELATEDINFORMATION]
>
>* **Kickstart Guides** These guides explain the initial steps to take once you have decided to begin integrating with Adobe Primetime authentication.
>* **Programmer Integration Guide** This is a lower level technical guide for Programmers, directed primarily to the software engineers who code and test the applications and systems involved in the integration.
>* [Overview For MVPDs](/help/authentication/mvpd-overview.md) This provides a similar level of conceptual information as in this Programmer overview, but is directed toward MVPDs.
-->
