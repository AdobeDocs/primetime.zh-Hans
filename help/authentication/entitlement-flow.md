---
title: 程序员授权流程
description: 程序员授权流程
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1822'
ht-degree: 0%

---


# 程序员授权流程 {#prog-entitlement-flow}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## 概述 {#overview}

本文档从程序员的角度介绍了基本的权利流程。  有关TVE基本集成之外的功能和用例的信息，请参见 [程序员用例](/help/authentication/programmer-use-cases.md).

Adobe Primetime身份验证通过为双方提供安全、一致的接口来调节程序员和MVPD之间的权利流。  在程序员方面，Primetime身份验证提供了两种一般类型的权利界面：

1. AccessEnabler — 一种客户端组件，为可呈现网页（如Web应用程序、智能手机/平板电脑应用程序）的设备上的应用程序提供API库。
2. 无客户端API — 适用于无法呈现网页的设备（例如机顶盒、游戏机、智能电视）的RESTful Web服务。 呈现网页的要求来自MVPD要求用户在MVPD的网站上进行身份验证。

除了此处介绍的平台中性概述外，此处还提供了特定于客户端的API概述：无客户端API文档。 AccessEnabler在支持的平台(Web上的AS/JS、iOS上的Objective-C和Android上的Java)上本地运行。 AccessEnabler API在支持的平台中保持一致。 所有不支持AccessEnabler的平台都使用相同的无客户端API。

对于这两种类型的界面，Primetime身份验证可安全地调整程序员应用程序和用户MVPD之间的权利流：

![](assets/prog-entitlement-flow.png)


*图：Adobe Primetime身份验证生态系统*

>[!IMPORTANT]
>
>上图中请注意，授权流程中有一部分未通过Adobe Primetime身份验证服务器：MVPD登录。 用户必须登录其MVPD的登录页面。 由于此要求，在无法呈现网页的设备上，程序员应用程序必须引导用户切换到能够使用Web的设备，以使用其MVPD登录，然后用户在权利流程的剩余时间返回原始设备。

## 授权流程 {#entitlement-flow}

基本权利流程有四个不同的子流：

1. [启动流程](/help/authentication/entitlement-flow.md#startup)
1. [身份验证流程](/help/authentication/entitlement-flow.md#authentication)
1. [授权流程](/help/authentication/entitlement-flow.md#authorization)
1. [注销流程](/help/authentication/entitlement-flow.md#logout)

在用户首次访问程序员网站时，权利流按上述顺序进行。 但是，在后续访问中，根据身份验证和授权令牌是否过期，或根据查看策略，用户可能只经过一个或两个子流。

### 启动流程 {#startup}

建立程序员和设备的身份，执行初始化任务。 这是所有后续授权调用的先决条件。

**AccessEnabler**

* **`setRequestor()`**  — 通过AccessEnalber（扩展）和Adobe Primetime身份验证服务器建立您的标识。 此调用是授权流程其余部分的前导。 例如，在JavaScript中：

   ```JavaScript
     /* Define the requestor ID (Programmer/aggregator ID). */
       var requestorID = "sample_requestor_Id";
       ...
       // Callback indicating that the AccessEnabler swf has initialized
       function swfLoaded() {
           // AccessEnabler is loaded so we can use the API function it provides
           accessEnablerObject.setRequestor(requestorID); 
       ...
       }
   ```

**无客户端API**

* **`\<REGGIE\_FQDN\>/reggie/v1/{requestorId}/regcode`**  — 根据平台的不同，在应用程序调用重新编码之前，可能需要完成先决任务。 请参阅 **无客户端API文档** 以了解详细信息。 例如，Xbox平台要求您在调用regcode之前完成规定的安全步骤。

### 身份验证流程 {#authentication}

成功的身份验证会生成与设备和请求者绑定的AuthN令牌。 成功身份验证是授权的先决条件。

**AccessEnabler**

* `checkAuthentication()`  — 检查本地令牌缓存中是否存在有效的缓存身份验证令牌，而无需实际触发完整的身份验证流程。 这会触发 `setAuthenticationStatus()` 回调函数。
* `getAuthentication()`  — 启动完整的身份验证流程。 如果成功，Adobe Primetime身份验证会生成一个AuthN令牌，并在客户端上缓存该令牌。 用户登录其选定的MVPD站点，该站点在iFrame、弹出窗口或Web视图中显示，具体取决于平台。 这会触发displayProviderDialog()。

**无客户端API**

* `<FQDN>/.../checkauthn`  — 的Web服务版本 `checkAuthentication()` 上。
* `<FQDN>/.../config`  — 将MVPD的列表返回到第2屏幕应用程序。
* `<FQDN>/.../authenticate`  — 从第2屏幕应用程序启动身份验证流程，将用户重定向到其选定的MVPD以进行登录。 如果成功，Adobe Primetime身份验证会生成一个AuthN令牌并将其存储在服务器上，然后用户返回到其原始设备以完成授权流程。

如果以下两点为true，则认为AuthN令牌有效：

* AuthN令牌未过期
* 与AuthN令牌关联的MVPD位于当前请求者ID允许的MVPD列表上

#### 通用AccessEnabler初始身份验证工作流 {#generic-ae-initial-authn-flow}

1. 您的应用程序通过调用 `getAuthentication()`，用于检查有效的缓存身份验证令牌。 此方法具有可选 `redirectURL` 参数；如果不为 `redirectURL`，成功验证后，会将用户返回到初始化身份验证的URL。
1. AccessEnabler确定当前身份验证状态。 如果用户当前已通过身份验证，则AccessEnabler会调用 `setAuthenticationStatus()` 回调函数，传递表示成功的身份验证状态。
1. 如果用户未进行身份验证，AccessEnabler将继续验证流程，方法是确定用户上次的验证尝试是否与给定MVPD成功。 如果MVPD ID已缓存，并且 `canAuthenticate` 标记为true，或者使用 `setSelectedProvider()`，则系统不会在MVPD选择对话框中提示用户。 验证流程会继续使用MVPD的缓存值（即，上次成功验证期间使用的相同MVPD）。 系统会向后端服务器发起网络调用，用户将被重定向到MVPD登录页面。

1. 如果没有缓存MVPD ID，并且未使用 `setSelectedProvider()` 或 `canAuthenticate` 标记设置为false， `displayProviderDialog()` 调用回调。 此回调将指导您的应用程序创建UI，以向用户显示可供选择的MVPD列表。 提供了MVPD对象数组，其中包含构建MVPD选择器所需的信息。 每个MVPD对象都描述一个MVPD实体，并包含MVPD的ID和可找到MVPD徽标的URL等信息。

1. 选择MVPD后，您的应用程序必须通知AccessEnabler用户选择的。 对于非Flash客户端，一旦用户选择所需的MVPD，您将通过对 `setSelectedProvider()` 方法。 Flash客户端而是派送共享 `MVPDEvent` 类型“`mvpdSelection`“ ”，传递选定的提供程序。

1. 当AccessEnabler获知用户的MVPD选择时，将向后端服务器发起网络调用，并将用户重定向到MVPD登录页面。

1. 在验证工作流中， AccessEnabler与Adobe Primetime验证和所选MVPD通信，以请求用户的凭据（用户ID和密码）并验证其身份。 虽然某些MVPD会重定向到其自己的网站进行登录，但其他MVPD会要求您在iFrame中显示其登录页面。 如果客户选择其中一个MVPD，则您的页面必须包含用于创建iFrame的回调。<!-- For more information on creating a login iFrame, see  [Managing the Login IFrame](https://tve.helpdocsonline.com/managing-the-login-iframe)-->.

1. 用户成功登录后， AccessEnabler会检索身份验证令牌，并通知您的应用程序身份验证流程已完成。 AccessEnabler将调用 `setAuthenticationStatus()` 状态代码为1的回调，表示成功。 如果在执行这些步骤期间出错，则 `setAuthenticationStatus()` 回调使用状态代码为0触发，表示身份验证失败以及相应的错误代码。

>[!IMPORTANT]
>Comcast是当前唯一不提供徽标静态URL的MVPD。 程序员应从 [XFINITY开发人员门户](https://developers.xfinity.com/products/tv-everywhere).

### 授权流程 {#authorization}

授权是查看受保护内容的先决条件。 成功授权会生成一个AuthZ令牌，以及一个为安全目的而提供给程序员应用程序的短暂媒体令牌。 请注意，要支持授权工作流，您必须先执行了必要的请求者设置，并集成了 [媒体令牌验证器](/help/authentication/media-token-verifier-int.md). 完成后，您可以启动授权。

当用户请求访问受保护的资源时，您的应用程序会启动授权。 您传递一个资源ID，以指定所请求的资源（例如，渠道、剧集等）。 您的应用程序首先会检查是否存储了身份验证令牌。 如果找不到，则启动身份验证过程。

**AccessEnabler**

* `checkAuthorization()`  — 在未启动完全授权流程的情况下检查授权。 它通常用于更新程序员应用程序UI中显示的状态信息。

* `getAuthorization()`  — 启动完整授权流程。

您提供以下回调函数来处理授权调用的结果：

* `setToken()`  — 如果先前验证成功且授权成功， AccessEnabler会调用 `setToken()` 回调函数，传递短期媒体令牌，指示成功结束Adobe Primetime身份验证授权流程。 (在允许用户查看受保护的内容之前，程序员的应用程序使用媒体令牌验证器检查媒体令牌的有效性。

* `tokenRequestFailed()`  — 如果用户未获得所请求资源的授权（或者如果查询因任何其他原因而失败），则AccessEnabler将调用此回调函数（加上您自己的错误报告函数），并传递有关失败的详细信息。

**无客户端API**

* `\<FQDN\>/.../authorize`  — 启动完整授权流程。

#### 通用AccessEnabler授权工作流 {#generic-ae-authr-wf}

1. 提供回调函数，该函数使用 `setReqestor()`. 成功下载AccessEnabler后，将调用此回调函数。

1. 调用 `getAuthorization()` 当用户请求访问受保护的资源时。 使用 `getAuthorization()`，传递指定所请求资源的资源ID（例如，渠道、剧集等）。 AccessEnabler会查找要与授权请求一起传递的缓存身份验证令牌。 如果找不到，则启动验证流程。
1. 提供回调函数以处理授权结果：

   * `setToken()`  — 如果授权成功或用户之前已获得授权，则Access Enabler将通过调用 `setToken()` 回调函数，传递短暂的授权令牌。

   * `tokenRequestFailed()`  — 如果用户未获得所请求资源的授权（或者如果查询因任何其他原因而失败）， AccessEnabler将调用您注册的任何错误报告函数，以及 `tokenRequestFailed()` 回调，传递有关失败的详细信息。

### 注销流程 {#logout}

清除与当前用户的授权流程关联的令牌和其他数据。

**AccessEnabler**

* `logout()`

**无客户端API**

* `\<FQDN\>/.../logout`

## 了解AccessEnabler行为 {#ae-behavior}

所有AccessEnabler API调用都是异步的（API引用中记录了一个例外）。 您可以调用API任意次数，但是无法强烈保证，由调用触发的操作将以发出调用的相同顺序完成。 (这的例外是当前Flash Player运行时；不是多线程的，它将确保调用 *do* 按调用顺序完成。)

为了区分响应，并能够将响应与调用配对，所有回调都会回复其输入参数。 这包括 `setToken()` 和`tokenRequestFailed()`，最终由 `checkAuthorization()`. (对于 `checkAuthorization()` 回调时，使用的资源会回调。) 利用此功能，您可以区分与哪个调用对应的响应。 要使用此功能，您可以编码如下内容：

```JavaScript
    for each (resource in ["TNT", "CNN", "TBS", "AdultSwim"] ) {
         ae.checkAuthorization(resource);
    }
    
    // Success callback
    function setToken(resource, token) {
         // Use "resource" to figure 
         // out which checkAuthorization
         // call triggered this response
    }
    
    // Old error callback
    function tokenRequestFailed(resource, error, details) {
         // use "resource" to figure
         // out in response to which
         // checkAuthorization call
         // this was triggered
    }
    
    // Error callback using new error api
    ae.bind("errorEvent',"errorHandler");
    
    function errorHandler(error) {
         if(error.resource) {        
              // Use error.resource to figure
              // which checkAuthorization call
              // triggered this response
         }
    }
```

### AE行为常见问题解答 {#ae-beh-faq}

**问题。 如果在第一个调用完成之前再次调用AccessEnabler，会发生什么情况？**

当执行第二调用（异步通信）时，将继续执行第一调用。

**问题。 AccessEnabler支持的同时调用数是否最大？**

AccessEnabler代码中未明确设置任何限制，因此您仅受可用系统资源以及MVPD容量的限制。

<!--

>[!MORELIKETHIS]
>
>*   [Programmer use cases](/help/authentication/programmer-use-cases.md)
>*   Error Reporting
>**Platform Cookbooks:**
>*   Clientless integration cookbook
>*   iOS Integration Cookbook
>*   Android Integration Cookbook
>*   JavaScript Integration Cookbook
>*   ActionScript Integration Cookbook
>*   Windows 8 Integration Cookbook
>*   AIR Native Extension Overview
-->