---
title: 程序员概述
description: 程序员概述
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '4272'
ht-degree: 0%

---


# 程序员概述 {#programmers-overview}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## 简介 {#introduction}

此概述面向计划将Adobe®传递集成到其网站或应用程序的内容提供商（程序员）。 有关包括Kickstart和集成指南在内的其他文档，请参阅下面的相关信息。

如今，您的查看者可以随时随地上网，并请求您（程序员）直接访问受保护的内容。 他们可能想观看一次性的活动，或者他们可能正在寻求你正在播放的整个电视剧的观看权。

但是，在允许访问受保护的内容之前，您必须确定客户是否有权查看该内容。 他们是否订购了多渠道视频节目分发服务(MVPD)? 如果是，那么该订阅是否包含您的编程？

对程序员而言，确定查看者的权利并非总是那么简单。 MVPD拥有其客户的标识数据和访问权限。  此外，尝试访问受保护内容的查看者订阅了各种MVPD（每个MVPD具有不同的系统），因此，确定查看者对受保护内容的权利会很快变得复杂，并且在技术上具有挑战性：

![](assets/user-ent-by-progr.png)

*图：由程序员直接确定的用户权利*

Adobe Primetime TV Everywhere身份验证可安全地协调节目制作员和MVPD之间的授权交易。 Adobe Primetime身份验证使程序员能够轻松、快速、安全地向有效客户提供受保护的内容：

![](assets/user-ent-mediatedby-authn.png)

*图：由Adobe Primetime身份验证中介的用户权利*

Adobe Primetime身份验证在与参与的MVPD的交换中充当代理，因此您可以通过一致的跨站点界面向您的查看者展示。 Adobe Primetime身份验证还允许您为查看者提供单点登录(SSO)身份验证和授权。 对所有参与服务的身份验证和授权进行跟踪，以便订阅者在其自己的系统上进行首次身份验证后无需再次登录。

* **身份验证**  — 通过MVPD确认给定用户是已知客户的过程。
* **授权**  — 通过MVPD确认已验证的用户对指定资源有效订阅的过程。

### Adobe Primetime身份验证的工作原理 {#HowItWorks}

程序员的内容查看应用程序使用Access Enabler客户端组件或无客户端API的RESTful Web服务（对于非Web功能设备，如智能电视、游戏机、机顶盒等）与Adobe Primetime身份验证进行交互。 Access Enabler在用户系统上运行，方便了所有授权工作流。  当客户访问您的网站并请求受保护的内容时，将从其托管站点Adobe下载Access Enabler组件。  Adobe Primetime身份验证服务器托管在无客户端解决方案中使用的RESTful Web服务。

Adobe Primetime身份验证可处理实际的权利工作流程，同时提供您用于：

* 设置您的身份。 (程序员是Adobe Primetime身份验证授权流程中的“请求者”。)
* 使用特定MVPD验证用户。  (MVPD是Adobe Primetime身份验证授权流程中的“身份提供者”或“IdP”。)
* 使用MVPD为特定资源授权用户。
* 注销用户。

程序员负责执行以下操作的高级网页或播放器应用程序：

* 实施用户界面
* 与Access Enabler或无客户端API Web服务交互

Adobe Primetime身份验证的目标是为程序员和MVPD创建一种简单的模块化方式来处理权利验证。

## 了解令牌 {#understanding-tokens}

Adobe Primetime身份验证授权解决方案的核心是生成在身份验证和授权工作流成功完成时创建的特定数据段。 这些数据称为令牌。 令牌的有效期有限；当令牌过期时，需要通过重新启动身份验证和授权工作流来重新发布令牌。

有关令牌的详细信息，请参阅以下部分：

* [令牌类型](#token-types)
* [令牌存储](#token-storage)
* [令牌安全](#token-security)
* [令牌共享](#token-sharing)

### 令牌类型 {#token-types}

在身份验证和授权工作流程期间，会发布三种类型的令牌。 AuthN和AuthZ令牌是“长寿命的”，可为用户提供持续的查看体验。 媒体令牌是一个短期令牌，可支持通过流跳转来防止欺诈的行业最佳实践。 程序员根据与MVPD达成的协议，为每种类型的令牌指定生存时间(TTL)值。 程序员会决定TTL的价值，以便最好地服务于您的企业和客户。

* **AuthN令牌** （“长寿”）：成功验证后，Adobe Primetime身份验证会创建与请求设备和全局唯一标识符(GUID)都关联的AuthN令牌。
   * Adobe Primetime身份验证会将AuthN令牌发送到Access Enabler，Access Enabler会在客户端系统上安全地缓存该令牌。  虽然AuthN令牌已存在且未过期，但它适用于使用Adobe Primetime身份验证的所有应用程序。 Access Enabler对授权流程使用AuthN令牌。
   * 在任何给定时间，都只缓存一个AuthN令牌。 只要颁发了新的AuthN令牌且旧令牌已存在，Adobe Primetime身份验证就会覆盖缓存的令牌。
* **AuthZ令牌** （“长寿”）：成功授权后，Adobe Primetime身份验证会创建与请求设备和特定受保护资源关联的AuthZ令牌。  受保护的资源由唯一的资源ID标识。
   * Adobe Primetime身份验证会将AuthZ令牌发送到Access Enabler，Access Enabler会在本地系统上安全地缓存该令牌。 然后，访问启用程序使用AuthZ令牌创建用于实际查看访问的短期媒体令牌。
   * 在任何给定时间，每个资源只缓存一个AuthZ令牌。 Adobe Primetime身份验证可以缓存多个AuthZ令牌，但前提是这些令牌与不同资源关联。 每当发出新的AuthZ令牌且同一资源已存在旧令牌时，Adobe Primetime身份验证都会覆盖缓存的令牌。
* **媒体令牌** （“短寿”）：Access Enabler使用AuthZ令牌生成短暂(默认值：7分钟)媒体令牌。 此时，会认为已发生成功的播放请求。
   * 在提供对受保护资源的访问权限之前，您的媒体服务器必须使用Adobe Primetime身份验证组件（媒体令牌验证器）来验证媒体令牌。
   * 由于媒体令牌未绑定到设备，因此其生命周期会显着缩短(默认：7分钟)，而不是长寿命的AuthN和AuthZ令牌。
   * 短暂的媒体令牌仅限于一次性使用，从不缓存。 每次调用授权API时，都会从Adobe Primetime身份验证服务器中检索该API。

### 令牌存储 {#token-storage}

Access Enabler将长期令牌（AuthN和AuthZ）存储在特定于其环境的位置：

* **Flash10.1** （或更高）：长期使用的令牌将存储为本地共享对象。
* **HTML5**:长期使用的令牌可安全地保留在HTML5浏览器的本地存储中。
* **iOS**:长期令牌存储在永久性粘贴板上，其他Adobe Primetime身份验证客户端应用程序可在该粘贴板上访问这些令牌。
* **Android**:长期令牌存储在共享的数据库文件中，其他Adobe Primetime身份验证客户端应用程序可在此文件中访问这些令牌。
* **无客户端API设备**:令牌存储在Primetime身份验证服务器上。

### 令牌安全 {#token-security}

Adobe Primetime身份验证服务器使用设备ID（从设备的硬件特性派生）对所有长期使用的令牌进行数字签名。 数字签名的生成、保护和验证方式因环境而异：

* **Flash10.1** （或更高） — 设备ID依赖于设备凭据，该凭据是从Adobe个性化服务器颁发的唯一证书。 此安全性等同于FAXS DRM技术。 此服务器端验证会将令牌中的唯一设备ID与设备凭据(从Flash Player到Adobe Primetime身份验证的安全通信)进行比较。 设备凭据还可标识FAXS客户端版本以及向其颁发的Flash Player(或AIR)版本。 与HTML5相比，设备绑定更强，因此令牌的生存时间(TTL)通常会随着Flash而延长。
* **HTML5**  — 设备在客户端上是个性化的。 它使用通过JavaScript提供的特性来生成伪设备ID，该ID包括浏览器和操作系统版本、IP地址和浏览器Cookie GUID（全局唯一标识符）。 将此令牌设备ID与设备的当前伪设备ID进行比较。 由于IP地址在正常使用期间可能会发生更改，即使在同一会话中，Adobe Primetime身份验证也会将HTML5令牌存储在以下两个位置：localStorage和sessionStorage。 如果IP发生更改，并且sessionStorage令牌仍然有效，则会维护会话。 使用HTML5时，设备绑定不那么强，因此令牌的TTL通常比Flash的TTL短。
* **本机客户端** (iOS和Android) — 长期使用的令牌包含本机设备ID个性化信息，因此绑定到请求的设备。 身份验证和授权请求通过HTTPS发送，设备ID信息由Access Enabler库进行数字签名，然后再发送到后端服务器。 在服务器端，设备ID信息将根据其关联的数字签名进行验证。
* **无客户端API客户端**  — 无客户端API解决方案具有其一组安全协议，这些协议涉及对所有API调用进行数字签名。 在授权流程期间生成的令牌安全地存储在Adobe Primetime身份验证服务器上。

Adobe Primetime身份验证将验证每个长期使用的令牌，以确保访问内容的设备与发布令牌的设备相同。 对于所有令牌，客户端验证可确保数字签名完整无缺，并保留令牌的完整性。 当设备ID验证失败时，身份验证会话失效，并提示用户重新登录，这将重置令牌。

### 令牌共享 {#token-sharing}

不同平台上的应用程序不共享令牌。 出现此情况的原因有很多，包括：

* 如 [令牌存储](#token-storage)，则存储令牌的方法会因平台而异(例如，Flash的本地共享对象、 WebStorage for JavaScript)。
* 不同平台的令牌安全程度不同。 例如，Flash令牌会使用FAXS强烈绑定到设备。 纯JavaScript环境中的令牌的DRM支持级别与Flash中的令牌不同。  与Flash应用程序共享JS令牌可能会增加使用更安全的环境时使用不安全令牌的可能性。

## 程序员集成生命周期 {#prog-integ-lifecycle}

![](assets/progr-flow-int-lifecycle.png)

*图：将认证与程序员网站和应用程序集成*


## 逻辑流 {#logical-flows}

### 权利流程图 {#chart}

以下流程图介绍了确认权利的整个过程(使用Adobe Primetime身份验证访问启用程序客户端组件):

![](assets/ent-flowchart.png)

*图：确认权利的过程*

### 身份验证步骤 {#authn-steps}

以下步骤演示了Adobe Primetime身份验证流程的示例。  这是授权流程的一部分，程序员在该流程中确定用户是否是MVPD的有效客户。  在此方案中，用户是MVPD的有效订阅者。  用户正在尝试使用程序员的Flash应用程序查看受保护的内容：

1. 用户浏览到程序员网页，该网页将程序员的Flash应用程序和Adobe Primetime身份验证访问启用程序组件加载到用户的计算机上。 Flash应用程序使用Access Enabler通过Adobe Primetime身份验证来设置程序员的标识，而Adobe Primetime身份验证将Access Enabler作为程序员的配置和状态数据的前缀（“请求者”）。 在执行任何其他API调用之前，Access Enabler必须从服务器接收此数据。 技术说明：程序员使用Access Enabler&#39;s `setRequestor()` 方法；有关详细信息，请参阅 [程序员集成指南](/help/authentication/programmer-integration-guide-overview.md).
1. 当用户尝试查看程序员的受保护内容时，程序员的应用程序向用户显示MVPD列表，用户从中选择提供商。
1. 用户将被重定向到Adobe Primetime身份验证服务器，其中加密了 [SAML](https://en.wikipedia.org/wiki/Security_Assertion_Markup_Language) 将创建用户选择的MVPD请求。 此请求将作为代表程序员向MVPD发送的身份验证请求。 根据MVPD的系统，用户的浏览器随后会被重定向到MVPD的站点以登录，或者在程序员的应用程序中创建登录iFrame。
1. 无论是在哪种情况下（重定向还是iFrame），MVPD都会接受请求并显示其登录页面。
1. 用户使用MVPD登录，MVPD将验证用户作为付费客户的状态，然后MVPD创建自己的HTTP会话。
1. 验证用户后，MVPD会创建一个响应（SAML和加密），MVPD会将该响应发送回Adobe Primetime身份验证。
1. Adobe Primetime身份验证接收MVPD响应，发现有Adobe Primetime身份验证HTTP会话打开，验证来自MVPD的SAML响应，并重定向回程序员网站。
1. 重新加载程序员站点，重新加载Access Enabler，程序员再次调用setRequestor()。  对setRequestor()的第二次调用是必需的，因为当前配置已更改 — 现在存在一个标记，该标记通知Access Enabler AuthN令牌正在等待在服务器上生成。
1. Access Enabler会发现有待处理的身份验证，并从Adobe Primetime身份验证服务器请求令牌。 通过调用Flash Player的DRM功能，可从服务器中检索令牌。
1. AuthN令牌存储在程序员的Flash PlayerLSO缓存中；身份验证现已完成，会话在Adobe Primetime身份验证服务器上被销毁。

### 授权步骤 {#authz-steps}

从 [身份验证步骤](#authn-steps):

1. 当用户尝试访问程序员保护的内容时，程序员的应用程序首先在用户的本地计算机或设备上检查AuthN令牌。  如果令牌不在，则 [身份验证步骤](#authn-steps) 之后是。  如果AuthN令牌存在，则授权流程将随程序员应用程序发起对Access Enabler的调用而进行，该调用请求获取用户对受保护内容特定项目的查看权限。
1. 受保护内容的特定项目由“资源标识符”表示。  这可以是一个简单的字符串或更复杂的结构，但无论如何，资源标识符的性质是在程序员和MVPD之间提前商定的。  程序员的应用程序将资源标识符传递给Access Enabler。  Access Enabler在用户的本地计算机或设备上检查AuthZ令牌。  如果AuthZ令牌不在，则Access Enabler会将请求传递到后端Adobe Primetime身份验证服务器。
1. Adobe Primetime身份验证服务器使用标准化协议与MVPD授权端点通信。  如果MVPD响应指示用户有权查看受保护的内容，则Adobe Primetime身份验证服务器将创建一个AuthZ令牌，并将其传递回Access Enabler，Access Enabler将AuthZ令牌存储在用户计算机上。
1. 通过将AuthZ令牌存储在用户的机器或设备上，程序员的应用程序调用Access Enabler以从Adobe Primetime身份验证服务器获取媒体令牌，并将该令牌提供给程序员的应用程序。
1. 最后，程序员的应用程序使用媒体令牌验证器组件来确认正确的用户正在查看正确的内容，并且在媒体令牌就位后，允许用户查看受保护的内容。


## 注册和初始化 {#reg-and-init}

使用Adobe Primetime身份验证的第一步是向Adobe或经Adobe Primetime身份验证授权的合作伙伴注册。

注册时，您会提供一个将从中与Adobe Primetime身份验证通信的域列表。 例如，Turner广播系统域包括tbs.com和tnt.tv作为Adobe Primetime身份验证注册域。 这些内容站点中的每个站点都有权访问Adobe Primetime身份验证，并且被分配了自己的请求者ID（例如，“TBS”和“TNT”）。 如果您决定添加其他网站，则必须通知Adobe其他域名，以便将其置于允许的域列表中，并获得其他请求者ID。

>[!WARNING]
>
>在测试集成时，请确保测试服务器位于您打算在生产中使用的注册域上。 来自未列入白名单的域的请求（甚至是测试请求）将被忽略。 例如，如果您请求在生产中使用domain.com，请确保在domain.com、test.domain.com和staging.domain.com下部署测试集成。
>
>即使将域列入白名单，URL中包含用户名和/或密码的请求也会被忽略。 示例： `//username@registered-domain/`

请求者ID在与Adobe Primetime身份验证的Access Enabler客户端组件的所有通信中唯一标识程序员的客户端。 与程序员关联的所有Adobe Primetime身份验证静态数据都与此ID有关键。

>[!TIP]
>
>除了请求者ID之外，在注册时，您还会收到Access Enabler客户端组件和媒体令牌验证器的功能URL。

## 集成步骤 {#integration-steps}

>[!TIP]
>
>如果您将Adobe的Open Source Media Framework(“OSMF”)用于媒体播放器开发，则使用Adobe Primetime身份验证的最快捷方式是集成OSMF插件 *（已弃用）* 输入你的玩家代码。
>
><!--For details, see [Adobe Primetime authentication Plugin For OSMF](https://tve.helpdocsonline.com/9-2-2) in the Programmer Integration Guide.-->

1. [请求者设置](#requestor)
1. [处理身份验证和授权](#authn-authz)
1. [支持单次注销](#ssl)

### 1.请求者设置 {#requestor}

#### 1a。 注册Adobe

您的第一步是向Adobe或Adobe Primetime身份验证授权合作伙伴注册。  注册时，您会获得一个或多个全局唯一标识符(GUID)。 您发出的每个GUID都与允许从中访问Adobe Primetime身份验证的域关联。 您为请求域传递一个GUID（称为请求者ID），以注册您与Access Enabler交互的每个会话的身份。 有关详细信息，请参阅 [注册和初始化](#reg-and-init) 中。

#### 1b。 初始Access Enabler集成

下一步是将Access Enabler集成到您现有的媒体播放器应用程序或网页中：

* 您可以嵌入Flash版本， `AccessEnabler.swf`，或者，您也可以直接将其嵌入到网页的HTML中。 您可以在ActionScript或JavaScript中与Access EnablerSWF通信。 基本API是ActionScript的，但如果您希望使用JavaScript，则可以在您的页面上包含完整的包装器库。
* 对于非Flash环境，您可以：
   * 使用HTML5/JavaScript版本AccessEnabler.js，并通过JavaScript API与其通信
   * 使用AIR Native Extension for Adobe Primetime身份验证将本机代码与内置ActionScript类结合使用
   * 使用Access Enabler库(iOS或Android)的一个本机客户端版本

### 2.处理身份验证和授权 {#authn-authz}

#### 2a。 与Access Enabler通信

Access Enabler与网页或播放器应用程序之间的通信是异步的。 您的应用程序会调用Access Enabler方法，Access Enabler会通过您在Access Enabler库中注册的回调进行响应。

* 当您的应用程序发出授权请求时，如果本地系统上尚不存在有效的AuthN令牌，则Access Enabler会自动启动身份验证请求。 当身份验证成功时，用户的AuthN令牌将存储在本地，以便他们无需再次登录。 如果他们在任何其他上下文（例如，通过MVPD网站或通过其他程序员）中通过Adobe Primetime身份验证成功进行了身份验证，则Access Enabler有权访问本地AuthN令牌，并且不需要额外的身份验证。
* 当用户尝试访问您的受保护内容时，您向Access Enabler发送授权请求。 验证（或启动）验证后，Access Enabler(通过Adobe Primetime验证服务器)与MVPD联系，以确定客户是否有权查看受保护的内容。 您的应用程序只需将请求发送到Access Enabler，然后处理响应（授权成功或失败）。 如果授权成功，则AuthZ令牌将存储在客户端系统上。  最后，您的应用程序会收到一个用于您自己的授权过程的短暂的媒体令牌。

>[!NOTE]
>
>* 身份验证作为SAML Exchange，在作为服务提供商(SP)的Adobe Primetime身份验证和作为身份提供商(IdP)的MVPD之间进行。
>
>* 授权使用Adobe Primetime身份验证(SP)与MVPD(IdP)之间的后通道（服务器到服务器）Web服务交换。



#### 2b。 提供授权用户界面 {#entitlement-ui}

您为用户提供了自己的UI以访问您的内容。 MVPD提供了一些元素，例如实际登录过程，某些元素也可作为Adobe Primetime身份验证的一部分提供。 您至少应执行以下操作：

* **实施MVPD选择界面，以便新用户识别其MVPD并首次登录**. Access Enabler提供了基本的用户界面，为客户提供了MVPD选项并启动登录过程。 对于生产环境，您必须实施自己的MVPD选择器对话框。 有些MVPD重定向到自己的网站进行登录，有些MVPD要求其登录页面显示在iFrame中。 您必须实施用于创建此iFrame的回调，以处理用户的MVPD在iFrame中显示其登录页面的情况。
* **识别受保护的内容**. 受保护的内容需要授权才能访问。 您的界面应指示哪些内容受保护以及哪些内容已获得授权。  授权状态通常以“已解锁”和“已锁定”图标来表示。
* **显示用户已通过身份验证**. 您应将用户的身份验证状态作为用于标识受保护内容的任何方式的一部分。 您可以查询Access Enabler以确定客户是否已经过身份验证。

#### 2c。 集成媒体令牌验证器 {#int-media-token-ver}

您必须将Adobe Primetime身份验证媒体令牌验证器组件集成到媒体服务器中。  这样，您的现有令牌验证器就可以识别通过成功授权从Adobe Primetime身份验证提供的短期媒体令牌。 在用户提供对受保护内容的访问权限之前，媒体令牌验证器会将媒体令牌验证为最后一个安全步骤。 在Adobe中注册时，您将收到从中下载媒体令牌验证器的位置。

### 3.支持单次注销 {#ssl}

在大多数情况下，您的媒体播放器负责通过简单的Access Enabler API处理用户注销。 调用logout()时， Access Enabler会执行以下操作：

* 注销当前用户
* 清除已注销用户的所有身份验证和授权信息
* 从用户的本地系统中删除所有AuthN和AuthZ令牌

如果用户将计算机闲置足够长的时间，使其令牌过期，则用户仍可以返回会话并成功启动注销。 Adobe Primetime身份验证可确保删除所有令牌，并通知MVPD删除其会话。

从未与Adobe Primetime身份验证集成的站点启动注销时，MVPD可以通过浏览器重定向调用Adobe Primetime身份验证单次注销服务。

## 了解用户ID {#user-ids}

从概念上讲，启动授权流程的每个用户都与单个唯一的用户ID关联。  但是，在授权流程中，一个用户ID可以通过不同的方式显示，具体取决于您从哪个API获取该ID。

短媒体令牌中的sessionGUID是UserID的安全形式，可通过sendTrackingData()调用使用。   在所有当前集成中，这是跨时间和设备的用户的永久GUID，但该GUID的源以MVPD的SAML响应中的UserID开头。   但是，某些MVPD将来可能会改变主意，开始发送临时GUID。  如果程序员希望确保AuthN响应中的MVPD源用户ID是永久性的，则他们在与MVPD的协议中应该安排该ID。

以下是用户ID在Adobe Primetime身份验证API中的不同显示方式：

* `sendTrackingData()` GUID属性 — 这是MVPD用户ID的Adobe哈希版本。  该ID经过哈希处理，因此无法跟踪该用户ID从MVPD返回到源。   此ID是唯一的，通常是永久性的，但无法与MVPD共享，以将特定的使用行为与MVPD侧面的使用行为进行比较。   它没有进行数字签名，因此不会在防欺诈方面不可欺骗，但它对于分析是足够好的。  在Adobe Primetime身份验证在AuthN/AuthZ流中生成的所有事件上，都提供了此形式的用户ID客户端。
* 短媒体令牌 `sessionGUID` 属性 — 与UserID通过 `sendTrackingData()`但是，这个文件是经过数字签名以保护其完整性的。  这样，该值就足以用于并发使用情况的欺诈跟踪。 在使用我们的验证器库后，将在服务器端处理该数据流，在将视频流发布到客户端之前，可以分析是否存在欺诈模式。  要完成这些任务，都由程序员来决定。
* `getMetadata() userID `属性 — 此属性将允许Adobe向程序员公开实际的源MVPD用户ID。 它将使用程序员提供的证书中的公钥进行加密，以便不会向客户公开。 这为程序员提供了MVPD中的实际用户ID，因此它可以直接与MVPD进行帐户关联或欺诈调查。

**最后**

* MVPD用户ID通常是永久性的唯一ID，虽然没有保证 **从MVPD生成，并在成功验证时传递到Adobe**. 在所有网络中，它通常都保持一致，但有些例外。
* MVPD用户ID不包含PII，也不是帐号。 由于我们已与所有MVPD一起验证没有发送PII的信息，因此无需以加密形式公开该信息。


用户ID的使用方式取决于用例：

* 如果您需要它进行跟踪/分析，最实际的位置是从 `sendTrackingData()`.
* 如果需要在服务器端获取流发布、欺诈或操作数据，可以从媒体令牌验证器获取该数据。
* 如果您需要它来关联帐户和进行更深入的欺诈，请咨询您的Adobe联系人以获取相关信息。

<!--
>[!RELATEDINFORMATION]
>
>* **Kickstart Guides** These guides explain the initial steps to take once you have decided to begin integrating with Adobe Primetime authentication.
>* **Programmer Integration Guide** This is a lower level technical guide for Programmers, directed primarily to the software engineers who code and test the applications and systems involved in the integration.
>* [Overview For MVPDs](/help/authentication/mvpd-overview.md) This provides a similar level of conceptual information as in this Programmer overview, but is directed toward MVPDs.
-->