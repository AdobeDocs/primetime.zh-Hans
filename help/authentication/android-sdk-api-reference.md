---
title: Android SDK API参考
description: Android SDK API参考
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '4517'
ht-degree: 0%

---



# Android SDK API参考 {#android-sdk-api-reference}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## 简介 {#intro}

本文档详细介绍了Android SDK为Adobe Primetime身份验证公开的方法和回调，Adobe Primetime身份验证版本1.7及更高版本支持此方法和回调。 AccessEnabler.h和EntitlementDelegate.h头文件中定义了此处介绍的方法和回调函数。

请参阅 [https://tve.zendesk.com/hc/en-us/articles/204963219-Android-Native-AccessEnabler-Library](https://tve.zendesk.com/hc/en-us/articles/204963219-Android-Native-AccessEnabler-Library) 以了解最新的Android AccessEnabler SDK。 


**注意：** Adobe Primetime身份验证团队鼓励您仅使用Adobe Primetime身份验证 *公共* API:

- 提供公共API *经过充分测试* 所有受支持的客户端类型。 对于任何公共功能，我们确保每个客户端类型都具有相关方法的相应版本。</span>
- 公共API必须尽可能稳定，才能支持向后兼容性并确保合作伙伴集成不会中断。 但是，对于 *non* — 公共API，我们保留在未来任何时刻更改其签名的权利。 如果您遇到某个特定流程，该流程无法通过当前公共Adobe Primetime身份验证API调用的组合进行支持，最好让我们知道。 考虑到您的需求，我们可以修改公共API并提供一个稳定的解决方案。

## Android API {#api}

- [getInstance](#getInstance)
- [setOptions](#setOptions)
- [setRequestor](#setRequestor)
- [setRequestorComplete](#setRequestorComplete)
- [checkAuthentication](#checkAuthN)
- [getAuthentication](#getAuthN)
- [displayProviderDialog](#displayProviderDialog)
- [setSelectedProvider](#setSelectedProvider)
- [navigateToUrl](#navigagteToUrl)
- [getAuthenticationToken](#getAuthNToken)
- [setAuthenticationStatus](#setAuthNStatus)
- 预授权
- [checkAuthorization](#checkAuthZ)
- [getAuthorization](#getAuthZ)
- [setToken](#setToken)
- [tokenRequestFailed](#tokenRequestFailed)
- [注销](#logout)
- [getSelectedProvider](#getSelectedProvider)
- [selectedProvider](#selectedProvider)
- [getMetadata](#getMetadata)
- [setMetadataStatus](#setMetadaStatus)
- [getVersion](#getVersion)

### Factory.getInstance {#getInstance}

**描述：** 实例化Access Enabler对象。 每个应用程序实例应有一个Access Enabler实例。

| API调用：构造函数 |
| --- |
| **公共静态** AccessEnabler **getInstance**（上下文appContext，字符串softwareStatement，字符串redirectUrl）<br>        **扔** AccessEnablerException <br><br>**公共静态** AccessEnabler getInstance(ContextAppContext， String env_url， String softwareStatement， String redirectUrl)<br>**扔** AccessEnablerException |

**可用性：** v3.1.2+

**参数：**

- *appContext*:Android应用程序上下文。
- env\_url:要使用Adobe测试环境进行测试，可以将env\_url设置为“sp.auth-staging.adobe.com”

**已弃用：**

```
    public static AccessEnabler getInstance(Context appContext)
        throws AccessEnablerException
```



### setRequestor {#setRequestor}

**描述：** 确定程序员的身份。 在向Adobe Primetime身份验证系统的Adobe注册时，每个程序员被分配一个唯一ID。 在处理SSO和远程令牌时，当应用程序处于后台时，身份验证状态可能会发生更改，当应用程序进入前台时，可以再次调用setRequestor以与系统状态同步（如果启用了SSO，则获取远程令牌，如果同时发生注销，则删除本地令牌）。

服务器响应包含MVPD列表以及附加到程序员身份的一些配置信息。 服务器响应由Access Enabler代码在内部使用。 只有操作的状态（即SUCCESS/FAIL）会通过setRequestorComplete()回调函数显示给您的应用程序。

如果 *url* 参数，则生成的网络调用将定向默认的服务提供商URL:Adobe发布/生产环境。

如果为 *url* 参数，则生成的网络调用将定向 *url* 参数。 所有配置请求都在单独的线程中同时触发。 编译MVPD列表时，优先使用第一个响应者。 对于列表中的每个MVPD，访问启用码会记住相关服务提供商的URL。 所有后续授权请求都会被定向到与配置阶段中与目标MVPD配对的服务提供商关联的URL。

| API调用：请求者配置 |
| --- |
| ```public void setRequestor(String requestorId)``` |

**可用性：** v3.0+

| API调用：请求者配置 |
| --- |
| ```public void setRequestor(String requestorId, ArrayList<String> urls)``` |
**可用性：** v3.0+


**参数：**

- *requestorID*:与程序员关联的唯一ID。 在您首次使用Adobe Primetime身份验证服务进行注册时，将由Adobe分配的唯一ID传递到您的网站。

- *signedRequestorID*:使用您的私钥进行数字签名的请求者ID的副本。 <!--For more details. see [Registering Native Clients](http://tve.helpdocsonline.com/registering-native-clients)-->.

- *url*:可选参数；默认情况下，使用Adobe服务提供商(http://sp.auth.adobe.com/)。 此数组允许您为由Adobe提供的身份验证和授权服务指定端点（可能出于调试目的而使用不同的实例）。 您可以使用它指定多个Adobe Primetime身份验证服务提供程序实例。 这样做时，MVPD列表由所有服务提供商的端点组成。 每个MVPD都与最快的服务提供商关联；即首先响应并支持该MVPD的提供商。

**触发的回调：** `setRequestorComplete()`

已弃用：

    public void setRequestor(String requestorId， String signedRequestorId)
    
    public void setRequestor(String requestorId， String signedRequestorId， ArrayList)&lt;string> url)

[返回到Android API...](#api)

### setRequestorComplete {#setRequestorComplete}

**描述：** 由Access Enabler触发的回调，该回调会通知您的应用程序配置阶段已完成。 这表示应用程序可以开始发出授权请求。 在配置阶段完成之前，应用程序不会发出任何授权请求。

| 回调：请求者配置完成 |
| --- |
| java public void setRequestorComplete(int status) |

**可用性：** v1.0+

**参数：**

- *状态*:可以采用以下值之一：
   - SDK \>= 3.4.0
      - `AccessEnablerConstants.ACCESS_ENABLER_STATUS_SUCCESS`  — 配置阶段成功完成
      - `AccessEnablerConstants.ACCESS_ENABLER_STATUS_ERROR`  — 配置阶段失败
   - SDK \&lt; 3.4
      - `AccessEnabler.ACCESS_ENABLER_STATUS_SUCCESS`  — 配置阶段成功完成
      - `AccessEnabler.ACCESS_ENABLER_STATUS_ERROR`  — 配置阶段失败

**触发者：** `setRequestor()`

[返回到Android API...](#api)

### setOptions {#setOptions}

**描述：** 配置全局SDK选项。 它接受 **地图\&lt;string string=&quot;&quot;>** 作为参数。 映射中的值将随SDK发起的每次网络调用一起传递到服务器。

这些值将独立于当前流（身份验证/授权）传递到服务器。 如果要更改值，可以随时调用此方法。

| API调用：setOptions |
| --- |
| public void setOptions(HashMap&lt;string string=&quot;&quot;> 选项) |

**可用性：** v1.9.2+

**参数：**

- *选项*:地图&lt;string string=&quot;&quot;> 包含全局SDK选项。 目前，提供了以下选项：
   - **applicationProfile**  — 它可用于根据此值进行服务器配置。
   - **ap_vi** -Marketing CloudvisitorID。 此值稍后可用于高级分析报表。
   - **ap_ai**  — 广告ID
   - **device_info**  — 客户端信息，如下所述： [传递客户信息设备连接和应用](/help/authentication/passing-client-information-device-connection-and-application.md).

[回到顶……](#apis)


### checkAuthentication {#checkAuthN}

**描述：** 检查身份验证状态。 它通过在本地令牌存储空间中搜索有效的身份验证令牌来执行此操作。 调用此方法不执行网络调用。 应用程序使用它查询用户的身份验证状态并相应地更新UI（即更新登录/注销UI）。 认证状态通过 [*setAuthenticationStatus()*](#setAuthNStatus) 回调。

如果MVPD支持“每个请求者进行身份验证”功能，则可以在设备上存储多个身份验证令牌。  有关此功能的详细信息，请参阅 [缓存准则](#$caching) 部分。

| API调用：检查身份验证状态 |
| --- |
| public void checkAuthentication() |

**可用性：** v1.0+

**参数：** 无

**触发的回调：** `setAuthenticationStatus()`

[返回到Android API...](#api)


### getAuthentication {#getAuthN}

**描述：** 启动完整身份验证工作流。 首先检查身份验证状态。 如果尚未进行身份验证，则启动身份验证流状态机：

- 如果上次身份验证尝试成功，则会跳过MVPD选择阶段，并且 [*navigateToUrl()*](#navigagteToUrl) 会触发回调。 应用程序使用此回调实例化向用户显示MVPD登录页面的WebView控件。
- 如果上次身份验证尝试失败或用户明确注销，则 [*displayProviderDialog()*](#displayProviderDialog) 会触发回调。 您的应用程序使用此回调来显示MVPD选择UI。 此外，您的应用程序还需要通过 [setSelectedProvider()](#setSelectedProvider) 方法。

当用户的凭据在MVPD登录页面上验证时，您的应用程序需要监控用户在MVPD登录页面进行身份验证时发生的多次重定向操作。 输入正确的凭据后，WebView控件将被重定向到 *AccessEnabler.ADOBEPASS\_REDIRECT\_URL* 常量。 WebView不会加载此URL。 应用程序必须截取此URL并将此事件解释为登录阶段已完成的信号。 然后，它应将控制权交给Access Enabler，以完成身份验证流程(通过调用 *getAuthenticationToken()* 方法)。

如果MVPD支持“每个请求者进行身份验证”功能，则可以在设备上存储多个身份验证令牌（每个程序员存储一个）。  有关此功能的详细信息，请参阅 [缓存准则](#$caching) 部分。

最后，通过 *setAuthenticationStatus()* 回调。



| API调用：启动验证流程 |
| --- |
| public void getAuthentication() |

**可用性：** v1.0+

| API调用：启动验证流程 |
| --- |
| public void getAuthentication(boolean forceAuthN， Map&lt;string object=&quot;&quot;> genericData) |

**可用性：** v1.8+

**参数：**

- *forceAuthn*:一个标记，用于指定是否应启动身份验证流程，而不考虑用户是否已经过身份验证。
- *数据*:包含要发送到付费电视通行证服务的键值对的映射。 Adobe可以使用此数据来启用将来的功能，而无需更改SDK。

**触发的回调：** `setAuthenticationStatus(), displayProviderDialog(), navigateToUrl(), sendTrackingData()`


[返回到Android API...](#api)

### displayProviderDialog {#displayProviderDialog}

**描述** 由Access Enabler触发的回调，用于通知应用程序需要实例化相应的UI元素，以允许用户选择所需的MVPD。 回调提供MVPD对象的列表，其中包含有助于正确构建选择UI面板的其他信息（例如指向MVPD徽标的URL、友好显示名称等）

用户选择所需的MVPD后，需要上层应用程序通过调用来恢复身份验证流程 *setSelectedProvider()* 并将与用户选择对应的MVPD的ID传递给MVPD。\
 
>[!NOTE]
>
> 中止身份验证流程
> </br></br>
> 请注意，在此点上，用户能够按“返回”按钮，这等同于身份验证流程的中止。 在这种情况下，您的应用程序需要调用 `setSelectedProvider()` 方法，传递 *null* 作为参数，为Access Enabler提供重置其身份验证状态机的机会。

| 回调：显示MVPD选择UI |
| --- |
| `public void displayProviderDialog(ArrayList<Mvpd> mvpds)` |

**可用性：** v1.0+

**参数**:

- *mvpd*:MVPD对象的列表，其中包含应用程序可用于构建MVPD选择UI元素的与MVPD相关的信息。

**触发者：** `getAuthentication(), getAuthorization()`

[返回到Android API...](#api)


### setSelectedProvider {#setSelectedProvider}

**描述：** 您的应用程序将调用此方法，以告知访问启用程序用户的MVPD选择。 应用程序可以使用此方法选择或更改用于身份验证的服务提供商。

如果所选MVPD是TempPass MVPD，则它将自动使用该MVPD进行身份验证，而无需随后调用getAuthentication()。

请注意，对于在getAuthentication()方法上提供额外参数的促销临时通行证，这是不可能的。

传递时 *null* 作为参数，Access Enabler假定用户已取消验证流程（即按“返回”按钮），并通过重置验证状态机和调用进行响应 *setAuthenticationStatus()* 使用 `AccessEnablerConstants.PROVIDER_NOT_SELECTED_ERROR` 错误代码。

| API调用：设置当前选定的提供程序 |
| --- |
| public void setSelectedProvider(String mvpdId) |

**可用性：** v1.0+

**参数：** 无

**触发的回调：** `setAuthenticationStatus(), sendTrackingData(), navigateToUrl()`

[返回到Android API...](#api)


### navigateToUrl {#navigagteToUrl}

**已弃用：** 从Android SDK 3.0开始，仅当设备上不存在Chrome自定义选项卡时，才使用navigateToUrl

**描述：** 由Access Enabler触发的回调，该回调通知应用程序需要向用户显示MVPD登录页面才能输入其凭据。 Access Enabler将作为参数传递MVPD登录页面的URL。 您的应用程序需要实例化WebView控件并将其定向到此URL。 此外，还需要应用程序来监视由WebView控件加载的URL，并截取针对由 `AccessEnabler.ADOBEPASS_REDIRECT_URL (deprecated)` 常量。 在发生此事件时，应用程序需要关闭或隐藏WebView控件，并通过调用 *getAuthenticationToken()* 方法。 Access Enabler通过从后端服务器检索身份验证令牌并将其存储在令牌存储中本地来完成身份验证流程。  

>[!WARNING]
>
> **中止身份验证流程**  <br>请注意，在此点上，用户能够按“返回”按钮，这等同于身份验证流程的中止。 在这种情况下，您的应用程序需要调用 _setSelectedProvider()_ 传递 _null_ 作为参数，并给Access Enabler重置其身份验证状态机的机会。

| 回调：显示MVPD登录页 |
| --- |
| public void navigateToUrl（字符串URL） |

**可用性：** v1.0+

**参数：**

- *url*:指向MVPD登录页面的URL

**触发者：** `getAuthentication(), setSelectedProvider()`

[返回到Android API...](#api)


### getAuthenticationToken {#getAuthNToken}

**已弃用：** 从Android SDK 3.0开始，由于Chrome自定义选项卡用于身份验证，因此不再从应用程序中使用此方法。

**描述：** 通过从后端服务器请求身份验证令牌来完成身份验证流程。 仅当托管MVPD登录页面的WebView控件被重定向到由 `AccessEnabler.ADOBEPASS_REDIRECT_URL` 常量。

| API调用：检索身份验证令牌 |
| --- |
| public void getAuthenticationToken() |

**可用性：** v1.0+

**参数：**

- *cookie*:在目标域上设置的Cookie（有关参考实施，请参阅SDK中的演示应用程序）。

**触发的回调：** `setAuthenticationStatus()`, `sendTrackingData()`

[返回到Android API...](#api)


### setAuthenticationStatus {#setAuthNStatus}

**描述：** 由Access Enabler触发的回调，用于通知应用程序身份验证流程的状态。 在很多情况下，此流可能会因用户交互或其他意外情况（如网络连接问题等）而失败。 此回调将通知应用程序身份验证流程的成功/失败状态，并在需要时提供有关失败原因的其他信息。

| 回调：报告身份验证流程的状态 |
| --- |
| public void setAuthenticationStatus(int status， String errorCode) |

**可用性：** v1.0+

**参数：**

- *状态*:可以采用以下值之一：
   - `AccessEnablerConstants.ACCESS_ENABLER_STATUS_SUCCESS`  — 身份验证流程成功完成
   - `AccessEnablerConstants.ACCESS_ENABLER_STATUS_ERROR`  — 验证流失
- *代码*:失败原因。 如果 *状态* is `AccessEnablerConstants.ACCESS_ENABLER_STATUS_SUCCESS`，则 *代码* 是空字符串(即，由 `AccessEnablerConstants.USER_AUTHENTICATED` 常量)。 如果失败，此参数可采用以下值之一：
   - `AccessEnablerConstants.USER_NOT_AUTHENTICATED_ERROR`  — 用户未通过身份验证。 响应 *checkAuthentication()* 方法调用。
   - `AccessEnablerConstants.PROVIDER_NOT_SELECTED_ERROR`  — 在上层应用程序通过后， AccessEnabler已重置身份验证状态机 *null* to `setSelectedProvider()` 中止身份验证流程。  用户可能已取消身份验证流程（即按“返回”按钮）。
   - `AccessEnablerConstants.GENERIC_AUTHENTICATION_ERROR`  — 身份验证流程因网络不可用或用户明确取消身份验证流程等原因而失败。

**触发者：** `checkAuthentication(), getAuthentication(), checkAuthorization()`

[返回到Android API...](#api)


### checkPreauthorizedResources {#checkPreauth}

>**已弃用：** 从Android SDK 3.6开始，预授权API正在替换checkPreauthorizedResources，以提供扩展的错误代码。 

**描述：** 应用程序使用此方法来确定用户是否已获得查看特定受保护资源的授权。 此方法的主要用途是检索用于装饰UI的信息（例如，通过锁图标和解锁图标指示访问状态）。

| API调用：设置当前选定的提供程序 |
| --- |
| `public void checkPreauthorizedResources(ArrayList<String> resources)` |

**可用性：** v1.3+

**参数：** 的 `resources` 参数是应检查授权的资源数组。 列表中的每个元素都应是一个表示资源ID的字符串。 资源ID受与 `getAuthorization()` 呼叫，即它应是程序员与MVPD或媒体RSS片段之间建立的商定值。

**触发了回调：** `preauthorizedResources()`

[返回到Android API...](#api)


### checkPreauthorizedResources {#checkPreauth2}

**已弃用：** 从Android SDK 3.6开始，预授权API正在替换checkPreauthorizedResources，以提供扩展的错误代码。 

**描述：** 应用程序使用此方法来确定用户是否已获得查看特定受保护资源的授权。 此方法的主要用途是检索用于装饰UI的信息（例如，通过锁图标和解锁图标指示访问状态）。

| API调用：设置当前选定的提供程序 |
| --- |
| `public void checkPreauthorizedResources(ArrayList<String> resources, boolean cache)` |

**可用性：** v3.1+

**参数：** 的 `resources` 参数是应检查授权的资源数组。 列表中的每个元素都应是一个表示资源ID的字符串。 资源ID受与 `getAuthorization()` 呼叫，即它应是程序员与MVPD或媒体RSS片段之间建立的商定值。

的 `cache` 参数指定是否可以使用缓存的预授权响应。 默认情况下，缓存为true，SDK将返回之前缓存的响应（如果可用）。

**触发了回调：** `preauthorizedResources()`

[返回到Android API...](#api)

### preauthorizedResources {#preauthResources}

**已弃用：** 从Android SDK 3.6开始，预授权API正在替换checkPreauthorizedResources，以提供扩展的错误代码。 不会在新API中调用preauthorizedResources回调函数。


**描述：** 由checkPreauthorizedResources()触发的回调。 提供已授权用户查看的资源列表。

| API调用：设置当前选定的提供程序 |
| --- |
| `public void checkPreauthorizedResources(ArrayList<String> resources)` |

**可用性：** v1.3+

**参数：** 的 `resources` 参数是用户已有权查看的资源数组。

**触发者：** `checkPreauthorizedResources()`

[返回到Android API...](#api)

### <span id="checkAuthZ"></span>checkAuthorization

**描述：** 应用程序使用此方法检查授权状态。 首先，检查身份验证状态。 如果未通过身份验证，则 *setTokenRequestFailed()* 会触发回调，且方法退出。 如果用户已通过身份验证，则还会触发授权流程。 请参阅 *getAuthorization()* 方法。

| API调用：检查授权状态 |
| --- |
| public void checkAuthorization(String resourceId) |

**可用性：** v1.0+

| API调用：检查授权状态 |
| --- |
| public void checkAuthorization(String resourceId， Map&lt;string object=&quot;&quot;> genericData) |

**可用性：** v1.8+

**参数：**

- *resourceId*:用户请求授权的资源的ID。
- *数据*:包含要发送到付费电视通行证服务的键值对的映射。 Adobe可以使用此数据来启用将来的功能，而无需更改SDK。

**触发的回调：** `tokenRequestFailed(), setToken(),sendTrackingData(), setAuthenticationStatus()`

[返回到Android API...](#api)


### <span id="getAuthZ"></span>getAuthorization

**描述：** 应用程序使用此方法来启动授权流程。 如果用户尚未进行身份验证，则还会启动身份验证流程。 如果用户通过了身份验证，则访问启用码将继续发出授权令牌（如果本地令牌缓存中不存在有效的授权令牌）和短期媒体令牌的请求。 一旦获得短媒体令牌，则认为授权流程已完成。 的 *setToken()* 触发回调，并将短媒体令牌作为参数交付到应用程序。 如果由于任何原因授权失败， *tokenRequestFailed()* 会触发回调，并提供错误代码和详细信息。

| API调用：启动授权流程 |
| --- |
| public void getAuthorization(String resourceId) |

**可用性：** v1.0+

| API调用：启动授权流程 |
| --- |
| public void getAuthorization(String resourceId， Map&lt;string object=&quot;&quot;> genericData) |

**可用性：** v1.8+

**参数：**

- *resourceId*:用户请求授权的资源的ID。
- *数据*:包含要发送到付费电视通行证服务的键值对的映射。 Adobe可以使用此数据来启用将来的功能，而无需更改SDK。 

**触发的回调：** `tokenRequestFailed(), setToken(), sendTrackingData()`

>[!WARNING]
>
> **已触发其他回调**  <br> 此方法还可以触发以下回调（如果还启动了身份验证流程）： *setAuthenticationStatus()*, *displayProviderDialog()*, *navigateToUrl()*

**注意：请尽可能使用checkAuthorization()而不是getAuthorization()。 getAuthorization()方法将启动完整的身份验证流程（如果用户未进行身份验证），这可能导致程序员方面实施复杂。**

[返回到Android API...](#api)


### setToken {#setToken}

**描述：** 由Access Enabler触发的回调，用于通知您的应用程序授权流程已成功完成。 短暂的媒体令牌也作为参数提供。

| 回调：授权流程已成功完成 |
| --- |
| public void setToken(String token， String resourceId) |

**可用性：** v1.0+

**参数：**

- *令牌*:短暂的媒体令牌
- *resourceId*:获得授权的资源

**触发者：** `checkAuthorization()`, `getAuthorization()`


[返回到Android API...](#api)

### tokenRequestFailed {#tokenRequestFailed}

**描述：** 由Access Enabler触发的回调，该回调会通知上层应用程序授权流程失败。

| 回调：授权流失败 |
| --- |
| public void tokenRequestFailed(String resourceId， <br>        字符串errorCode，字符串errorDescription) |

**可用性：** v1.0+

**参数：**

- *resourceId*:获得授权的资源
- *errorCode*:与失败方案关联的错误代码。 可能值：
   - `AccessEnablerConstants.USER_NOT_AUTHORIZED_ERROR`  — 用户无法为给定资源授权
- *errorDescription*:有关失败方案的其他详细信息。 如果此描述性字符串因任何原因不可用，则Adobe Primetime身份验证会发送一个空字符串 **(&quot;&quot;)**.

   MVPD可以使用此字符串传递自定义错误消息或与销售相关的消息。 例如，如果某个订阅者被拒绝授权某个资源，则MVPD可以发送消息，例如：“您当前无权访问包中的此渠道。 如果要升级您的资源包，请单击此处。” 该消息由Adobe Primetime身份验证通过此回调传递给程序员，程序员可以选择显示或忽略该消息。 Adobe Primetime身份验证还可以使用此参数提供可能导致错误的条件通知。 例如，“与提供商的授权服务通信时发生网络错误。”

**触发者：** `checkAuthorization(), getAuthorization()`

[返回到Android API...](#api)

### 注销 {#logout}

**描述：** 使用此方法启动注销流程。 注销是一系列HTTP重定向操作的结果，因为用户需要从Adobe Primetime身份验证服务器以及MVPD服务器中注销。 因此，无法通过Access Enabler库发出的简单HTTP请求来完成此流程。 SDK使用Chrome自定义选项卡来执行HTTP-redirect操作。 此流程对用户可见，完成后将关闭

| API调用：启动注销流程 |
| --- |
| 公共撤销注销() |

**可用性：** v1.0+

**参数：** 无

**触发的回调：**

- `navigateToUrl()` （适用于3.0之前的SDK版本）
- `setAuthenticationStatus()` （对于SDK版本> 3.0）


[返回到Android API...](#api)


### getSelectedProvider {#getSelectedProvider}

**描述：** 使用此方法可确定当前选择的提供程序。

| API调用：确定当前选定的MVPD |
| --- |
| public void getSelectedProvider() |

**可用性：** v1.0+

**参数：** 无

**触发的回调：** `selectedProvider()`

[返回到Android API...](#api)


### <span id="selectedProvider"></span>selectedProvider

**描述：** 由访问启用程序触发的回调，用于将有关当前选定MVPD的信息传送到应用程序。

| 回调：有关当前选定MVPD的信息 |
| --- |
| public void selectedProvider(Mvpd mvpd) |


**可用性：** v1.0+

**参数：**

- *mvpd*:包含有关当前选定MVPD的信息的对象

**触发者：** `getSelectedProvider()`

[返回到Android API...](#api)


### getMetadata {#getMetadata}

**描述：** 使用此方法可检索Access Enabler库作为元数据公开的信息。 应用程序可以通过提供复合MetadataKey对象来访问此信息。

| API调用：查询AccessEnabler以获取元数据 |
| --- |
| `public void getMetadata(MetadataKey metadataKey)` |

**可用性：** v1.0+

程序员可以使用两种类型的元数据：

- 静态元数据（身份验证令牌TTL、授权令牌TTL和设备ID） 
- 用户元数据（用户特定信息，如用户ID和邮政编码；在身份验证和/或授权流程期间从MVPD传递到用户设备）

**参数：**

- *metadataKey*:封装键和标记变量的数据结构，其含义如下：
   - 如果键为 `METADATA_KEY_USER_META` 和args包含名为=的SerializableNameValuePair对象 `METADATA_ARG_USER_META` 和值= `[metadata_name]`，则会为用户元数据创建查询。 可用用户元数据类型的当前列表：
      - `zip`  — 邮政编码

      - `householdID`  — 家庭标识符。 如果MVPD不支持子帐户，则与 `userID`.

      - `maxRating`  — 用户的家长评分上限

      - `userID`  — 用户标识符。 如果MVPD支持子帐户，并且用户不是主帐户， `userID` 将不同于 `householdID`.

      - `channelID`  — 用户有权查看的渠道列表
   - 如果键为 `METADATA_KEY_DEVICE_ID` 然后，进行查询以获取当前设备id。 请注意，此功能默认处于禁用状态，程序员应联系Adobe以获取有关启用和费用的信息。
   - 如果键为 `METADATA_KEY_TTL_AUTHZ` 和args包含名为=的SerializableNameValuePair对象 `METADATA_ARG_RESOURCE_ID` 和值= `[resource_id]`，则进行查询以获取与指定资源关联的授权令牌的过期时间。
   - 如果键为 `METADATA_KEY_TTL_AUTHN` 然后，进行查询以获取身份验证令牌过期时间。 

 

>[!NOTE]
>
>对于SDK 3.4.0，常量： `METADATA_KEY_USER_META, METADATA_KEY_DEVICE_ID, METADATA_KEY_TTL_AUTHZ, METADATA_KEY_TTL_AUTHN` 可从com.adobe.adobepass.accessenabler.api.profile.UserProfileService获取。



>[!NOTE]
>
>程序员可用的实际用户元数据取决于MVPD提供的内容。  此列表将进一步扩展，因为有新的元数据可用并添加到Adobe Primetime身份验证系统中。

**触发的回调：** [`setMetadataStatus()`](#setMetadaStatus)

**更多信息：** [用户元数据](/help/authentication/user-metadata-feature.md)

[返回到Android API...](#api)

### setMetadataStatus {#setMetadaStatus}

**描述：** 由Access Enabler触发的回调，该回调通过 *getMetadata()* 呼叫。

| 回调：元数据检索请求的结果 |
| --- |
| ```public void setMetadataStatus(MetadataKey key, MetadataStatus result)``` |

**可用性：** v1.0+

**参数：**

- *key*:MetadataKey对象，其中包含请求元数据值的键和关联的参数（有关引用实施，请参阅演示应用程序）。
- *结果*:包含所请求元数据的复合对象。 对象具有以下字段：
   - *simpleResult*:一个字符串，表示请求身份验证TTL、授权TTL或设备ID时的元数据值。 如果为用户元数据发出请求，则此值为null。

   - *userMetadataResult*:一个对象，其中包含JSON用户元数据有效负载的Java表示形式。\
      例如：

```json
          '{
          "street": "Main Avenue",
          "buildings": ["150", "320"]
          }'
```

已转换为Java，如下所示： 

```java
          Map("street" -> "Main Avenue", "buildings" -> List("150", "320")))
```

**用户元数据对象的实际结构类似于以下内容：**

```json
          {
              updated: 1334243471,
              encrypted: ["encryptedProp"],
              data: {
                  zip: ["12345", "34567"],
                  maxRating: { 
                      "MPAA": "PG-13",
                      "VCHIP": "TV-Y", 
                      "URL": "http://exam.pl/e/manage/ratings"
                  },
                  householdID: "3456",
                  userID: "BgSdasfsdk23/dsaf3+saASesadgfsShggssd=",
                  channelID: ["channel-1", "channel-2"]
              }
          }
```

对简单元数据（身份验证TTL、授权TTL或设备ID）发出请求时，此值为空。

- *加密*:布尔值，指定检索的元数据是否已加密。 此参数仅对于用户元数据请求而言很重要，对于静态元数据(例如：始终未加密的身份验证TTL)。 如果此参数设置为True，则程序员需通过使用白名单私钥(与在 [`setRequestor`](#setRequestor) 调用)。

**触发者：** [`getMetadata()`](#getMetadata)

**更多信息：** [用户元数据](/help/authentication/user-metadata-feature.md)


[返回到Android API...](#api)


### getVersion {#getVersion}

**描述：** 此方法可用于检索AccessEnabler库的版本。

| API调用：获取AccessEnabler版本 |
| --- |
| ```public static String getVersion()``` |


[返回到Android API...](#api)

</br>

## 跟踪事件 {#tracking}

Access Enabler会触发一个与授权流不一定相关的额外回调。 实施名为的事件跟踪回调函数 *sendTrackingData()* 是可选的，但它使应用程序能够跟踪特定事件并编译统计信息，如成功/失败的身份验证/授权尝试次数。 以下是 *sendTrackingData()* 回调：\
 

### sendTrackingData {#sendTrackingData}

**描述：** 由Access Enabler信令向应用程序触发的各种事件（如身份验证/授权流的完成/失败）的回调。 sendTrackingData()还会报告设备类型、Access Enabler客户端类型和操作系统。

>[!WARNING]
>
> 设备类型和操作系统是通过使用公共Java库([http://java.net/projects/user-agent-utils](http://java.net/projects/user-agent-utils))和用户代理字符串。 请注意，此信息仅作为一种将操作量度划分为设备类别的粗略方式提供，但该Adobe不会对错误结果负责。 请相应地使用新功能。


- 设备类型的可能值：
   - `computer`
   - `tablet`
   - `mobile`
   - `gameconsole`
   - `unknown`


- Access Enabler客户端类型的可能值：
   - `flash`
   - `html5`
   - `ios`
   - `android`

</br>

| 回调：跟踪事件 |
| --- |
| ```public void sendTrackingData(Event event, ArrayList<String> data)``` |

**可用性：** v1.0+

**参数：**

- *事件*:正在跟踪的事件。 有三种可能的跟踪事件类型：
   - **authorizationDetection:** 授权令牌请求随时返回(事件类型为 `EVENT_AUTHZ_DETECTION`)
   - **authenticationDetection:** 每次进行身份验证检查(事件类型为 `EVENT_AUTHN_DETECTION`)
   - **mvpdSelection:** 用户在MVPD选择表单中选择MVPD时(事件类型为 `EVENT_MVPD_SELECTION`)
- *数据*:与所报告事件关联的其他数据。 此数据以值列表的形式显示。

以下是解释 *数据*
数组：

- 对于事件类型 *`EVENT_AUTHN_DETECTION`:*
   - **0**  — 令牌请求是否成功(true/false)，如果上述为true:
   - **1** - MVPD ID字符串
   - **2** - GUID（md5哈希）
   - **3**  — 缓存中已有令牌(true/false)
   - **4**  — 设备类型
   - **5**  — 访问启用码客户端类型
   - **6**  — 操作系统类型

- 对于事件类型 `EVENT_AUTHZ_DETECTION`
   - **0**  — 令牌请求是否成功(true/false)，如果成功：
   - **1** - MVPD ID
   - **2** - GUID（md5哈希）
   - **3**  — 缓存中已有令牌(true/false)
   - **4**  — 错误
   - **5**  — 详细信息
   - **6**  — 设备类型
   - **7**  — 访问启用码客户端类型
   - **8**  — 操作系统类型

- 对于事件类型 `EVENT_MVPD_SELECTION`
   - **0**  — 当前选定MVPD的ID
   - **1**  — 设备类型
   - **2**  — 访问启用码客户端类型
   - **3**  — 操作系统类型

**触发者：** `checkAuthentication()`, `getAuthentication()`, `checkAuthorization()`, `getAuthorization()`, `setSelectedProvider()`

[返回到Android API...](#api)


<!--
## Related Information {#related}

- [Android Integration Cookbook](/help/authentication/android-sdk-cookbook.md)
- [Android Technical Overview](/help/authentication/android-sdk-overview.md)

-->
