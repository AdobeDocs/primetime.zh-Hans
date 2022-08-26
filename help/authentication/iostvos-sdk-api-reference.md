---
title: iOS/tvOS API参考
description: iOS/tvOS API参考
source-git-commit: 49d5d8c1de263bd63db642d71a5bbb926fa45f96
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# iOS/tvOS SDK API参考 {#iostvos-sdk-api-reference}

- [简介](#intro)
- [API参考](#apis)
- [跟踪事件](#tracking)
- [相关信息](#related)

>[!NOTE]
>
>**通知**:此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## 简介 {#intro}

本页介绍iOS/tvOS本机客户端为Adobe Primetime身份验证公开的方法和回调函数。 下面介绍的方法和回调函数在 `AccessEnabler.h` 和 `EntitlementDelegate.h` 头文件；您可以在iOS AccessEnabler SDK中的以下位置找到它们： `[SDK directory]/AccessEnabler/headers/api/`


相关文档：

- 有关基本的Primetime身份验证授权流程的说明，请参阅 [授权流程](https://tve.helpdocsonline.com/entitlement-flow).
- 有关如何使用此API实施Primetime身份验证权利流的分步说明，请参阅 [iOS集成指南](/help/authentication/iostvos-sdk-cookbook.md).
- 有关最新的iOS AccessEnabler SDK，请转到 <https://tve.zendesk.com/hc/en-us/articles/204963209-iOS-Native-AccessEnabler-Library>. 

 

**注意：** Adobe鼓励您仅使用Primetime身份验证 *公共* API:

- 公共API可用，并在所有受支持的客户端类型上经过充分测试。 对于任何公共功能，我们确保每个客户端类型都具有相关方法的相应版本。
- 公共API必须尽可能稳定，才能支持向后兼容性并确保合作伙伴集成不会中断。 但是，对于非公共API，我们保留在未来任何时刻更改其签名的权利。 如果您遇到某个特定流程，该流程无法通过当前公共Primetime身份验证API调用的组合获得支持，最好让我们知道。 考虑到您的需求，我们可以修改公共API并提供一个稳定的解决方案。

</br>

## API参考 {#apis}

- [init](#initWithSoftwareStatement):softwareStatement — 实例化AccessEnabler对象。
- **[已弃用]** [init](#init)  — 实例化AccessEnabler对象。
- [setOptions:options:](#setOptions)  — 配置全局SDK选项，如profileID或visitorID。
- [setRequestor:](#setReqV3)[requestorID](#setReqV3),[setRequestor:requestorID:服务提供商：](#setReqV3)  — 确定程序员的身份。
- **[已弃用]** [setRequestor:signedRequestorId:](#setReq), [setRequestor:signedRequestorId:服务提供商：](#setReq)  — 确定程序员的身份。
- **[已弃用]** [setRequestor:signedRequestorId:secret:publicKey](#setReq_tvos), [setRequestor:signedRequestorId:serviceProviders:secret:publicKey](#setReq_tvos)  — 确定程序员的身份。
- [setRequestorComplete:](#setReqComplete)  — 通知您的应用程序配置阶段已完成。
- [checkAuthentication](#checkAuthN)  — 检查当前用户的身份验证状态。
- [getAuthentication](#getAuthN), [getAuthentication:withData:](#getAuthN)  — 启动完整的身份验证工作流。
- [getAuthentication:filter](#getAuthN_filter),[ ](#getAuthN_filter)[getAuthentication:withData:](#getAuthN)[andFilter](#getAuthN_filter)  — 启动完整的身份验证工作流。
- [displayProviderDialog:](#dispProvDialog)  — 通知应用程序实例化相应的UI元素，以便用户选择MVPD。
- [setSelectedProvider:](#setSelProv)  — 将用户的MVPD选择通知AccessEnabler。
- [navigateToUrl:](#nav2url)  — 通知您的应用程序需要向用户显示MVPD登录页面。
- [navigateToUrl:useSVC:](#nav2urlSVC)  — 使用SFSafariViewController通知应用程序需要向用户显示MVPD登录页面
- [handleExternalURL:url](#handleExternalURL)  — 完成身份验证/注销流程。
- **[已弃用]** [getAuthenticationToken](#getAuthNToken)  — 从后端服务器请求身份验证令牌。
- [setAuthenticationStatus:errorCode:](#setAuthNStatus)  — 通知应用程序身份验证流程的状态。
- [checkPreauthorizedResources:](#checkPreauth)  — 确定用户是否已获得查看特定受保护资源的授权。
- [checkPreauthorizedResources:cache:](#checkPreauthCache)  — 确定用户是否已获得查看特定受保护资源的授权。
- [preauthorizedResources:](#preauthResources)  — 提供用户已经有权查看的资源列表。
- [checkAuthorization:](#checkAuthZ), [checkAuthorization:withData:](#checkAuthZ)  — 检查当前用户的授权状态。
- [getAuthorization:](#getAuthZ), [getAuthorization:withData:](#getAuthZ)  — 启动授权流程。
- [setToken:forResource:](#setToken)  — 通知您的应用程序授权流程已成功完成。
- [tokenRequestFailed:errorCode:errorDescription:](#tokenReqFailed)  — 通知您的应用程序授权流程失败。
- [注销](#logout)  — 启动注销流程。
- [getSelectedProvider](#getSelProv)  — 确定当前选定的提供程序。
- [selectedProvider:](#selProv)  — 将有关当前选定MVPD的信息传送到您的应用程序。
- [getMetadata:](#getMeta)  — 检索由AccessEnabler库作为元数据公开的信息。
- [presentTvProviderDialog:](#presentTvDialog)  — 通知您的应用程序以显示Apple SSO对话框。
- [discessTvProviderDialog:](#dismissTvDialog)  — 通知您的应用程序隐藏Apple SSO对话框。
- [setMetadataStatus:encrypted:forKey:andArguments:](#setMetaStatus)  — 传送由 [getMetadata:](#getMeta) 呼叫。
- [sendTrackingData:forEventType:](#sendTracking)  — 提供跟踪数据信息。
- [MVPD](#mvpd) - MVPD类。 [包含有关MVPD的信息]


### init:softwareStatement {#initWithSoftwareStatement}

**文件：** AccessEnabler/headers/AccessEnabler.h

**描述：** 实例化AccessEnabler对象。 每个应用程序实例应有一个AccessEnabler实例。

| **API调用：iOS AccessEnabler构造函数** |
| --- |
| `- (id) init:` <br> |
| `(NSString *)softwareStatement;` |


**可用性：** v3.0+

**参数：**

- softwareStatement:一个字符串，用于标识Adobe系统中的应用程序。 了解如何获取软件声明。

[回到顶……](#apis)



### init - [已弃用]{#init}

**文件：** AccessEnabler/headers/AccessEnabler.h

**描述：** 实例化AccessEnabler对象。 每个应用程序实例应有一个AccessEnabler实例。

| API调用：iOS AccessEnabler构造函数 |
| --- |
| ```- (id) init;``` |

**可用性：** v1.0+ **直到：** v3.0

**参数：** 无

 

[回到顶……](#apis)

</br>

### setOptions:options {#setOptions}

**文件：** AccessEnabler/headers/AccessEnabler.h

**描述：** 配置全局SDK选项。 它接受NSDictionary作为参数。 词典中的值将随SDK进行的每次网络调用一起传递到服务器。

**注意：** 这些值将独立于当前流（身份验证/授权）传递到服务器。 如果要更改值，可以随时调用此方法。

| API调用：setOptions |
| --- |
| ```- (void) setOptions:(NSDictionary *)options;``` |

**可用性：** v2.3.0+

**参数：**

- *选项*:包含全局SDK选项的NSDictionary。 目前，提供了以下选项：
   - **applicationProfile**  — 它可用于根据此值进行服务器配置。
   - **visitorID** -Marketing CloudvisitorID。 此值稍后可用于高级分析报表。
   - **handleSVC**  — 布尔值，指示程序员是否将处理SFSafariViewControllers。 请参阅 [iOS SDK 3.2+上的SFSafariViewController支持](https://tve.helpdocsonline.com/sfsafariviewcontroller-support-on-ios-sdk-3.2) 以了解更多详细信息。
      - 如果设置为 **false，** 该SDK将自动向最终用户显示SFSafariViewController。 SDK将进一步导航到MVPD登录页面URL。
      - 如果设置为 **真的，** SDK将 **NOT** 自动向最终用户显示SFSafariViewController。 SDK将进一步触发 **navigate(toUrl:{url}, useSVC:YES)**.
- **device\_info**  — 客户端信息，如下所述：
   <https://tve.helpdocsonline.com/passing-client-information>.

 

[回到顶……](#apis)


### setRequestor:requestorID， setRequestor:requestorID:服务提供商： {#setReqV3}

**文件：** AccessEnabler/headers/AccessEnabler.h

**描述：** 确定程序员的身份。 在向Primetime身份验证系统的Adobe注册时，每个程序员被分配一个唯一ID。 在处理SSO和远程令牌时，当应用程序处于后台时，身份验证状态可能会发生更改，当应用程序进入前台时，可以再次调用setRequestor以与系统状态同步（如果启用了SSO，则获取远程令牌，如果同时发生注销，则删除本地令牌）。


服务器响应包含MVPD列表以及附加到程序员身份的一些配置信息。 服务器响应由AccessEnabler代码在内部使用。 只有操作的状态（即SUCCESS/FAIL）才会通过 `setRequestorComplete:` 回调。

如果 `urls` 参数，则生成的网络调用将定向默认的服务提供商URL:Adobe版本/生产环境。


如果为 `urls` 参数，则生成的网络调用将定向 `urls` 参数。 所有配置请求都在单独的线程中同时触发。 编译MVPD列表时，优先使用第一个响应者。 对于列表中的每个MVPD， AccessEnabler会记住关联服务提供商的URL。 所有后续授权请求都会被定向到与配置阶段中与目标MVPD配对的服务提供商关联的URL。

| API调用：请求者配置 |
| --- |
| ```- (void) setRequestor:(NSString *)requestorID``` |


**可用性：** v3.0+

| API调用：请求者配置 |
| --- |
| `- (void) setRequestor:(NSString *)requestorID serviceProviders:(NSArray *)urls;` |


**可用性：** v3.0+

**参数：**

- *requestorID*:与程序员关联的唯一ID。 当您首次在Primetime身份验证服务中注册时，将由Adobe分配的唯一ID传递给您的网站。
- *url*:可选参数；默认情况下，使用Adobe服务提供商(http://sp.auth.adobe.com/)。 此数组允许您为由Adobe提供的身份验证和授权服务指定端点（可能出于调试目的而使用不同的实例）。 您可以使用它指定多个Primetime身份验证服务提供程序实例。 这样做时，MVPD列表由所有服务提供商的端点组成。 每个MVPD都与最快的服务提供商关联；即首先响应并支持该MVPD的提供商。

   **注意：** 如果在没有 `serviceProviders` 参数，则库将从默认服务提供程序(例如， `https://sp.auth.adobe.com` (用于生产配置文件，或https://sp.auth-staging.adobe.com用于暂存配置文件)。 如果 `serviceProviders` 参数时，该参数必须是URL的数组。将从所有指定的端点检索配置信息并进行合并。 如果重复信息存在于不同的服务提供商响应中，则冲突会被解决，以支持响应最快的服务器（即，优先使用响应时间最短的服务器）。

 

**触发的回调：** [`setRequestorComplete:`](#setReqComplete)

 

[回到顶……](#apis)

</br>

### setRequestor:setSignedRequestorId:, setRequestor:setSignedRequestorId:服务提供商： - [已弃用] {#setReq}

**文件：** AccessEnabler/headers/AccessEnabler.h

**描述：** 确定程序员的身份。 在向Primetime身份验证系统的Adobe注册时，每个程序员被分配一个唯一ID。 在处理SSO和远程令牌时，当应用程序处于后台时，身份验证状态可能会发生更改，当应用程序进入前台时，可以再次调用setRequestor以与系统状态同步（如果启用了SSO，则获取远程令牌，如果同时发生注销，则删除本地令牌）。

服务器响应包含MVPD列表以及附加到程序员身份的一些配置信息。 服务器响应由AccessEnabler代码在内部使用。 只有操作的状态（即SUCCESS/FAIL）才会通过 `setRequestorComplete:` 回调。

如果 `urls` 参数，则生成的网络调用将定向默认的服务提供商URL:Adobe版本/生产环境。

如果为 `urls` 参数，则生成的网络调用将定向 `urls` 参数。 所有配置请求都在单独的线程中同时触发。 编译MVPD列表时，优先使用第一个响应者。 对于列表中的每个MVPD， AccessEnabler会记住关联服务提供商的URL。 所有后续授权请求都会被定向到与配置阶段中与目标MVPD配对的服务提供商关联的URL。

| API调用：请求者配置 |
| --- |
| </br>`- (void) setRequestor:(NSString *)requestorID`</br>`signedRequestorID:(NSString *)signedRequestorID;` </br></br> |

**可用性：** v1.0+ **直到：** v3.0

| API调用：请求者配置 |
| --- |
| `- (void) setRequestor:(NSString *)requestorID ` <br> `       signedRequestorID:(NSString *)signedRequestorID` <br> `         serviceProviders:(NSArray *)urls;` |

**可用性：** v1.0+ **直到：** v3.0

**参数：**

- *requestorID*:与程序员关联的唯一ID。 在您首次使用Primetime身份验证服务进行注册时，将由Adobe分配的唯一ID传递到您的网站。
- *signedRequestorID*: **此参数存在于iOS AccessEnabler版本1.2及更高版本中。** 使用您的私钥进行数字签名的请求者ID的副本。 有关更多详细信息，请参阅 [注册本机客户端](https://tve.helpdocsonline.com/registering-native-clients).
- *url*:可选参数；默认情况下，使用Adobe服务提供商(http://sp.auth.adobe.com/)。 此数组允许您为由Adobe提供的身份验证和授权服务指定端点（可能出于调试目的而使用不同的实例）。 您可以使用它指定多个Primetime身份验证服务提供程序实例。 这样做时，MVPD列表由所有服务提供商的端点组成。 每个MVPD都与最快的服务提供商关联；即首先响应并支持该MVPD的提供商。

**注意：** 如果在没有 `serviceProviders` 参数时，库将从默认服务提供程序中检索配置(即： `https://sp.auth.adobe.com` ，或 `https://sp.auth-staging.adobe.com` （对于暂存配置文件）。 如果 `serviceProviders` 参数时，该参数必须是URL的数组。将从所有指定的端点检索配置信息并进行合并。 如果重复信息存在于不同的服务提供商响应中，则冲突会被解决，以支持响应最快的服务器（即，优先使用响应时间最短的服务器）。

**触发的回调：** [`setRequestorComplete:`](#setReqComplete)


[回到顶……](#apis)

### setRequestor:setSignedRequestorId:secret:publicKey， setRequestor:setSignedRequestorId:serviceProviders:secret:publicKey - [已弃用] {#setReq_tvos}

**文件：** AccessEnabler/headers/AccessEnabler.h

**描述：** 确定程序员的身份。 在向Primetime身份验证系统的Adobe注册时，每个程序员被分配一个唯一ID。 此设置在应用程序的生命周期内只应执行一次。

服务器响应包含MVPD列表以及附加到程序员身份的一些配置信息。 服务器响应由AccessEnabler代码在内部使用。 只有操作的状态（即SUCCESS/FAIL）才会通过 `setRequestorComplete:` 回调。

如果 `urls` 参数，则生成的网络调用将定向默认的服务提供商URL:Adobe版本/生产环境。

如果为 `urls` 参数，则生成的网络调用将定向 `urls` 参数。 所有配置请求都在单独的线程中同时触发。 编译MVPD列表时，优先使用第一个响应者。 对于列表中的每个MVPD， AccessEnabler会记住关联服务提供商的URL。 所有后续授权请求都会被定向到与配置阶段中与目标MVPD配对的服务提供商关联的URL。



<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API调用：请求者配置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setRequestor:(NSString *)requestorID 
    signedRequestorID:(NSString *)signedRequestorID
               secret:(NSString *)secret
            publicKey:(NSString *)publicKey;</code></pre></td>
</tr>
</tbody>
</table>


**可用性：** v2.0+ **直到：** v3.0

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API调用：请求者配置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setRequestor:(NSString *)requestorID 
    signedRequestorID:(NSString *)signedRequestorID 
     serviceProviders:(NSArray *)urls</code></pre>
<p><code class="sourceCode objectivec">               secret:(NSString *)secret</code></p>
<p><code class="sourceCode objectivec">            publicKey:(NSString *)publicKey;</code></p></td>
</tr>
</tbody>
</table>

**可用性：** v2.0+ **直到：** v3.0

**参数：**

- *requestorID*:与程序员关联的唯一ID。 在您首次使用Primetime身份验证服务进行注册时，将由Adobe分配的唯一ID传递到您的网站。
- *signedRequestorID*: **此参数存在于iOS AccessEnabler版本1.2及更高版本中。** 使用您的私钥进行数字签名的请求者ID的副本。 有关更多详细信息，请参阅 [注册本机客户端](https://tve.helpdocsonline.com/registering-native-clients).
- *url*:可选参数；默认情况下，使用Adobe服务提供商(http://sp.auth.adobe.com/)。 此数组允许您为由Adobe提供的身份验证和授权服务指定端点（可能出于调试目的而使用不同的实例）。 您可以使用它指定多个Primetime身份验证服务提供程序实例。 这样做时，MVPD列表由所有服务提供商的端点组成。 每个MVPD都与最快的服务提供商关联；即首先响应并支持该MVPD的提供商。
- secret和publicKey:用于对第二个屏幕调用进行签名的密钥和公钥。 有关详细信息，请参阅 [无客户关系文件](#create_dev).

如果在没有 `serviceProviders` 参数，则库将从默认服务提供程序(例如， `https://sp.auth.adobe.com` (用于生产配置文件，或https://sp.auth-staging.adobe.com用于暂存配置文件)。 如果 `serviceProviders` 参数时，该参数必须是URL的数组。将从所有指定的端点检索配置信息并进行合并。 如果重复信息存在于不同的服务提供商响应中，则冲突会被解决，以支持响应最快的服务器（即，优先使用响应时间最短的服务器）。

**触发的回调：** [`setRequestorComplete:`](#setReqComplete)

[回到顶……](#apis)

</br>

### setRequestorComplete: {#setReqComplete}

**文件：** AccessEnabler/headers/EntitlementDelegate.h

**描述** 由AccessEnabler触发的回调，用于通知您的应用程序配置阶段已完成。 这表示应用程序可以开始发出授权请求。 在配置阶段完成之前，应用程序不会发出任何授权请求。\
 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回调：请求者配置完成</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setRequestorComplete:(int)status;</code></pre></td>
</tr>
</tbody>
</table>


**可用性：** v1.0+

**参数**:

- *状态*:可以采用以下值之一：
   - `ACCESS_ENABLER_STATUS_SUCCESS`  — 配置阶段成功完成
   - `ACCESS_ENABLER_STATUS_ERROR`  — 配置阶段失败

**触发者：**
`setRequestor:setSignedRequestorId:, `[`setRequestor:setSignedRequestorId:serviceProviders:`](#setReq)

[回到顶……](#apis)

</br>

### checkAuthentication {#checkAuthN}

**文件：** AccessEnabler/headers/AccessEnabler.h

**描述：** 检查当前用户的身份验证状态。
它通过在本地令牌存储空间中搜索有效的身份验证令牌来执行此操作。 调用此方法不执行网络调用。 应用程序使用它来查询用户的身份验证状态并相应地更新UI（即更新登录/注销UI）。 认证状态通过 [`setAuthenticationStatus:errorCode:`](#setAuthNStatus) 回调。\
 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API调用：检查身份验证状态</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkAuthentication;</code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.0+

**参数：** 无

**触发的回调：**
[`setAuthenticationStatus:errorCode:`](#setAuthNStatus)

[回到顶……](#apis)

</br>

### getAuthentication， getAuthentication:withData: {#getAuthN}

**文件：** AccessEnabler/headers/AccessEnabler.h

**描述：** 启动完整身份验证工作流。 首先检查身份验证状态。 如果尚未进行身份验证，则启动身份验证流状态机：

- 如果上次身份验证尝试成功，则会跳过MVPD选择阶段，并且 [`navigateToUrl:`](#nav2url) 会触发回调。 应用程序使用此回调实例化向用户显示MVPD登录页面的WebView控件。 **[注意：自Access Enabler 1.5起，由于SDK存在限制，此功能不可用].**
- 如果上次身份验证尝试失败或用户明确注销，则 [`displayProviderDialog:`](#dispProvDialog) 会触发回调。 您的应用程序使用此回调来显示MVPD选择UI。 此外，您的应用程序还需要通过以下方式来恢复身份验证流程：通过 [`setSelectedProvider:`](#setSelProv) 方法。

当用户的凭据在MVPD登录页面上验证时，您的应用程序需要监控用户在MVPD登录页面进行身份验证时发生的多次重定向操作。 输入正确的凭据后，WebView控件将被重定向到 `ADOBEPASS_REDIRECT_URL` 常量。 WebView不会加载此URL。 应用程序必须截取此URL并将此事件解释为登录阶段已完成的信号。 然后，它应将控制权交给AccessEnabler，以完成验证流程(通过调用 [handleExternalURL](#handleExternalURL) 方法)。

最后，通过 [setAuthenticationStatus:errorCode:](#setAuthNStatus) 回调。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API调用：启动验证流程</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication;</code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.0+

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API调用：启动验证流程</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication:(BOOL)forceAuthn:
                  withData:(NSDictionary* )data;</code></pre>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

**可用性：** v1.9+

**参数：**

- *forceAuthn*:一个标记，用于指定是否应启动身份验证流程，而不考虑用户是否已经过身份验证。
- *数据*:包含要发送到付费电视通讯服务的键值对的字典。 Adobe可以使用此数据来启用将来的功能，而无需更改SDK。 

**触发的回调：** ` setAuthenticationStatus:errorCode:, `[`displayProviderDialog:`](#dispProvDialog)`,`` sendTrackingData:forEventType:`


[回到顶……](#apis)

</br>

### getAuthentication:filter， getAuthentication:withData:andFilter {#getAuthN_filter}

**文件：** AccessEnabler/headers/AccessEnabler.h

**描述：** 启动完整身份验证工作流。 首先检查身份验证状态。 如果尚未进行身份验证，则启动身份验证流状态机：

- [presentTvProviderDialog()](#presentTvDialog) 如果当前请求者至少有一个支持SSO的MVPD，则将调用。 如果没有MVPD支持SSO，则将开始经典身份验证流程，并忽略过滤器参数。
- 用户完成Apple SSO流程后 [discessTvProviderDialog()](#dismissTvDialog) 将触发，并完成身份验证过程。\
    

最后，通过 [setAuthenticationStatus:errorCode:](#setAuthNStatus) 回调。

**可用性：** v2.4+

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API调用：启动验证流程</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication:(NSDictionary *)filter;</code></pre></td>
</tr>
</tbody>
</table>

 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API调用：启动验证流程</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication:(BOOL)forceAuthn:
                  withData:(NSDictionary* )data
                 andFilter:(NSDictionary *)filter;</code></pre>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

**参数：**

- *forceAuthn*:一个标记，用于指定是否应启动身份验证流程，而不考虑用户是否已经过身份验证。
- *数据*:包含要发送到付费电视通讯服务的键值对的字典。 Adobe可以使用此数据来启用将来的功能，而无需更改SDK。 
- 过滤器：包含两个MVPD ID列表的词典，应显示在Apple SSO对话框中。 任何不支持单点登录(SSO)的MVPD将被忽略，但将遵守该顺序。 字典需要有两个键：
   - TV\_PROVIDERS:选取器中应显示的列表，其中包含所有MVPD
   - 特色\_TV\_PROVIDERS:选取器中应标记为具有的所有MVPD的列表。 此列表中的MVPD也必须在TV\_PROVIDERS列表中指定。

**可用性：** v2.0 - v2.3.1


<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API调用：启动验证流程</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication:(NSArray *)filter;</code></pre></td>
</tr>
</tbody>
</table>

 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API调用：启动验证流程</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthentication:(BOOL)forceAuthn:
                  withData:(NSDictionary* )data
                 andFilter:(NSArray *)filter;</code></pre>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

**参数：**

- *forceAuthn*:一个标记，用于指定是否应启动身份验证流程，而不考虑用户是否已经过身份验证。
- *数据*:包含要发送到付费电视通讯服务的键值对的字典。 Adobe可以使用此数据来启用将来的功能，而无需更改SDK。 
- 过滤器：应显示在Apple SSO对话框中的MVPD ID列表。 任何不支持单点登录(SSO)的MVPD将被忽略，但将遵守该顺序。

**触发的回调：** `setAuthenticationStatus:errorCode:, presentTvProviderDialog, dismissTvProviderDialog`


[回到顶……](#apis)

</br>

#### displayProviderDialog: {#dispProvDialog}

**文件：** AccessEnabler/headers/EntitlementDelegate.h

**描述** 由AccessEnabler触发的回调，用于通知应用程序需要实例化相应的UI元素，以允许用户选择所需的MVPD。 回调提供MVPD对象的列表，其中包含有助于正确构建选择UI面板的其他信息（例如指向MVPD徽标的URL、友好显示名称等）

用户选择所需的MVPD后，需要上层应用程序通过调用来恢复身份验证流程 `setSelectedProvider:` 并将与用户选择对应的MVPD的ID传递给MVPD。

**中止身份验证流程**  — 在此点上，用户能够按“返回”按钮，这等同于中止身份验证流程。 在这种情况下，您的应用程序需要调用 [setSelectedProvider:](#setSelProv) 方法，将null作为参数传递，以便让AccessEnabler有机会重置其身份验证状态机。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回调：显示MVPD选择UI</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) displayProviderDialog:(NSArray *)mvpds;</code></pre></td>
</tr>
</tbody>
</table>


**可用性：** v1.0+

**参数**:

- *mvpd*:包含应用程序可用于构建MVPD选择UI元素的MVPD相关信息的MVPD对象列表。

**触发者：** ` getAuthentication, `[getAuthentication:withData:](#getAuthN),` getAuthorization:, `[getAuthorization:withData:](#getAuthZ)


[回到顶……](#apis)

</br>

#### setSelectedProvider: {#setSelProv}

**文件：** AccessEnabler/headers/AccessEnabler.h

**描述：** 您的应用程序将调用此方法，以告知访问启用程序用户的MVPD选择。 应用程序可以使用此方法选择或更改用于身份验证的服务提供商。

如果所选MVPD是TempPass MVPD，则它将自动使用该MVPD进行身份验证，而无需随后调用getAuthentication()。

请注意，对于在getAuthentication()方法上提供额外参数的促销临时通行证，这是不可能的。

传递时 *null* 作为参数，Access Enabler假定用户已取消验证流程（即按“返回”按钮），并通过重置验证状态机和调用进行响应 [setAuthenticationStatus:errorCode:](#setAuthNStatus) 使用 `AccessEnabler.PROVIDER_NOT_SELECTED_ERROR` 错误代码。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API调用：设置当前选定的提供程序</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setSelectedProvider:(NSString *)mvpdId;</code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.0+

**参数：** 无

**触发的回调：** ` setAuthenticationStatus:errorCode:,sendTrackingData:forEventType:,  `[`navigateToUrl:`](#nav2url)

[回到顶……](#apis)

</br>

#### navigateToUrl: {#nav2url}

**文件：** AccessEnabler/headers/EntitlementDelegate.h

**描述：** 由AccessEnabler触发的回调，用于请求您的应用程序实例化UIWebView/WKWebView控制器并加载回调中提供的URL **`url`** 参数。 回调将传递 **`url`** 参数，表示身份验证端点的URL或注销端点的URL。

作为UIWebView/WKWebView` `控制器经过多次重定向，您的应用程序必须监控控制器的活动并检测其加载由定义的特定自定义URL的时间 `ADOBEPASS_REDIRECT_URL `常量(即 `adobepass://ios.app`)。 请注意，此特定的自定义URL实际上无效，并且不希望控制器实际加载它。 它只能被您的应用程序解释为验证或注销流程已完成并且关闭控制器是安全的信号。 当控制器加载此特定的自定义URL时，您的应用程序必须关闭UIWebView/WKWebView并调用AccessEnabler的 `handleExternalURL:url `API方法。

**注意：** 请注意，在身份验证流程中，这是用户能够按“返回”按钮的点，等同于身份验证流程的中止。 在这种情况下，您的应用程序需要调用 [setSelectedProvider:](#setSelProv) 传递 **`nil`** 作为参数，并给AccessEnabler重置其身份验证状态机的机会。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回调：显示MVPD登录页</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) navigateToUrl:(NSString *)url; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.0+

**参数**:

- *url*:指向MVPD登录页面的URL

**触发者：** [setSelectedProvider:](#setSelProv)

 

[回到顶……](#apis)

</br>

#### navigateToUrl:useSVC: {#nav2urlSVC}

**文件：** AccessEnabler/headers/EntitlementDelegate.h

**描述：** 由AccessEnabler触发的回调，而不是 `navigateToUrl:` 回调，以防您的应用程序之前通过启用手动Safari视图控制器(SVC)处理 [setOptions(\[&quot;handleSVC&quot;:true&quot;\])](#setOptions) 调用，并且仅在MVPD需要Safari视图控制器(SVC)时调用。 对于所有其他MVPD， `navigateToUrl:` 将调用callback。 请参阅[iOS SDK 3.2+上的SFSafariViewController支持](https://tve.helpdocsonline.com/sfsafariviewcontroller-support-on-ios-sdk-3.2) 有关如何管理Safari视图控制器(SVC)的详细信息。

与 `navigateToUrl:` 回调 `navigateToUrl:useSVC:` 由AccessEnabler触发，以请求应用程序实例化 `SFSafariViewController` 控制器和，以加载回调中提供的URL **`url`** 参数。 回调将传递 **`url`** 参数，表示身份验证端点的URL或注销端点的URL，以及 **`useSVC`** 参数，该参数指定应用程序必须使用 `SFSafariViewController`.

作为 `SFSafariViewController` 控制器经过多次重定向，您的应用程序必须监控控制器的活动并检测其加载由您定义的特定自定义URL的时间 `application's custom scheme` (例如** **`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`)。 请注意，此特定的自定义URL实际上无效，并且不希望控制器实际加载它。 它只能被您的应用程序解释为验证或注销流程已完成并且关闭控制器是安全的信号。 当控制器加载此特定的自定义URL时，您的应用程序必须关闭 `SFSafariViewController` 并调用AccessEnabler的 `handleExternalURL:url `API方法。

**注意：** 请注意，在身份验证流程中，这是用户能够按“返回”按钮的点，等同于身份验证流程的中止。 在这种情况下，您的应用程序需要调用 [setSelectedProvider:](#setSelProv) 传递 **`nil`** 作为参数，并给AccessEnabler重置其身份验证状态机的机会。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回调：在SFSafariViewController中显示MVPD登录页面</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>@optional
- (void) navigateToUrl:(NSString *)url useSVC:(BOOL)useSVC; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：**v 3.2+

**参数**:

- *url:* 指向MVPD登录页面的URL
- *useSVC:* 是否应在SFSafariViewController中加载url。

**触发者： **[setOptions:](#setOptions) 之前 [setSelectedProvider:](#setSelProv) 

[回到顶……](#apis)

</br>

#### handleExternalURL:url {#handleExternalURL}

**文件：** AccessEnabler/headers/AccessEnabler.h

**描述：** 应用程序将调用此方法以完成身份验证或注销流程。 在您的应用程序检测到 `UIWebView/WKWebView or SFSafariViewController` 控制器会被重定向到特定的自定义URL。 如果您的应用程序需要使用 `SFSafariViewController `控制器特定的自定义URL由 `application's custom scheme` (例如，`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`)，否则，此特定的自定义URL由 `ADOBEPASS_REDIRECT_URL `常量(即 `adobepass://ios.app`)。

在验证流程的情况下， AccessEnabler通过从后端服务器检索验证令牌并将其存储在令牌存储器本地来完成该流程。 AccessEnabler将通过调用 [`setAuthenticationStatus()`](http://tve.helpdocsonline.com/ios-technical-overview#setAuthNStatus) 状态代码为1的回调，表示成功。 如果在执行这些步骤期间出错，则 [`setAuthenticationStatus()`](http://tve.helpdocsonline.com/ios-technical-overview#setAuthNStatus) 回调使用状态代码为0触发，表示身份验证失败以及相应的错误代码。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API调用：完成验证或注销流程</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) handleExternalURL:(NSString *)url; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v3.0+

**参数：** 

- *url*:从 ` UIWebView/WKWebView or SFSafariViewController ` 控制为字符串。


**触发的回调：** `setAuthenticationStatus:errorCode, sendTrackingData:forEventType:`

[回到顶……](#apis)

</br>

#### getAuthenticationToken - [已弃用] {#getAuthNToken}

**文件：** AccessEnabler/headers/AccessEnabler.h

**描述：** 通过从后端服务器请求身份验证令牌来完成身份验证流程。 仅当托管MVPD登录页面的WebView控件被重定向到由 `ADOBEPASS_REDIRECT_URL` 常量。\
 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API调用：检索身份验证令牌</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthenticationToken; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.0+ **直到：** v3.0

**参数：** 无

**触发的回调：** `setAuthenticationStatus:errorCode,sendTrackingData:forEventType:`

[回到顶……](#apis)

&lt;/br

#### setAuthenticationStatus:errorCode: {#setAuthNStatus}

**文件：** AccessEnabler/headers/EntitlementDelegate.h

**描述** 由AccessEnabler触发的回调，用于通知应用程序身份验证流程的状态。 在很多情况下，此流可能会因用户交互或其他意外情况（如网络连接问题等）而失败。 此回调将通知应用程序身份验证流程的成功/失败状态，并在需要时提供有关失败原因的其他信息。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回调：报告身份验证流程的状态</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setAuthenticationStatus:(int)status 
                       errorCode:(NSString *)code; </code></pre></td>
</tr>
</tbody>
</table>


**可用性：** v1.0+

**参数**:

- *状态*:可以采用以下值之一：
   - `ACCESS_ENABLER_STATUS_SUCCESS`  — 身份验证流程成功完成
   - `ACCESS_ENABLER_STATUS_ERROR`  — 验证流失
- *代码*:失败原因。 如果 *状态* is `ACCESS_ENABLER_STATUS_SUCCESS`，则 *代码* 是空字符串(即，由 `USER_AUTHENTICATED` 常量)。 如果失败，此参数可采用以下值之一：
   - `USER_NOT_AUTHENTICATED_ERROR`  — 用户未通过身份验证。 响应 [checkAuthentication:](#checkAuthN) 方法调用。
   - `PROVIDER_NOT_SELECTED_ERROR`  — 在上层应用程序通过后， AccessEnabler已重置身份验证状态机 *null* to [`setSelectedProvider:`](#setSelProv) 中止身份验证流程。  用户可能已取消身份验证流程（即按“返回”按钮）。
   - `GENERIC_AUTHENTICATION_ERROR`  — 身份验证流程因网络不可用或用户明确取消身份验证流程等原因而失败。

**触发者：** ` checkAuthentication, getAuthentication, `[getAuthentication:withData:](#getAuthN),` checkAuthorization:, `[checkAuthorization:withData:](#checkAuthZ)

[回到顶……](#apis)

</br>

### checkPreauthorizedResources: {#checkPreauth}


**文件：** AccessEnabler/headers/AccessEnabler.h

**描述：** 应用程序使用此方法来确定用户是否已获得查看特定受保护资源的授权。 此方法的主要用途是检索用于装饰UI的信息 **（例如，通过锁图标和解锁图标指示访问状态）。**

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API调用：设置当前选定的提供程序</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkPreauthorizedResources:(NSArray *)resources; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.3+

**参数：**

- *资源：* 应检查授权的资源数组。 列表中的每个元素都应是一个表示资源ID的字符串。 资源ID受与调用中的资源ID相同的限制，即它应是程序员与MVPD或媒体RSS片段之间建立的商定值。

**触发了回调：** [`preauthorizedResources:`](#preauthResources)

[回到顶……](#apis)

</br>

### checkPreauthorizedResources:cache: {#checkPreauthCache}

**文件：** AccessEnabler/headers/AccessEnabler.h

**描述：** 应用程序使用此方法来确定用户是否已获得查看特定受保护资源的授权。 此方法的主要用途是检索用于装饰UI的信息（例如，通过锁图标和解锁图标指示访问状态）。 的 **缓存** 参数控制内部缓存是否用于解析资源。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API调用：设置当前选定的提供程序</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkPreauthorizedResources:(NSArray *)resources cache:(BOOL)cache; </code></pre></td>
</tr>
</tbody>
</table>

 

**可用性：** v3.1+

 

**参数：**

- *资源：* 应检查授权的资源数组。 列表中的每个元素都应是一个表示资源ID的字符串。 资源ID受与 `getAuthorization:` 呼叫，即它应是程序员与MVPD或媒体RSS片段之间建立的商定值。
- *缓存：* 布尔值，指定是否使用内部缓存来解析资源。 如果为false，则会绕过缓存，导致每次调用此API时都会调用服务器。

**触发了回调：** [`preauthorizedResources:`](#preauthResources)

[回到顶……](#apis)

</br>

### preauthorizedResources: {#preauthResources}

**文件：** AccessEnabler/headers/EntitlementDelegate.h

**描述：** 由触发的回调 `checkPreauthorizedResources:`. 提供已授权用户查看的资源列表。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API调用：设置当前选定的提供程序</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkPreauthorizedResources:(NSArray *)resources; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.3+

**参数：**

- *`resources`:已授权用户查看的资源数组。

**触发者：** [`checkPreauthorizedResources:`](#checkPreauth)

 

[回到顶……](#apis)

</br>

### checkAuthorization:,checkAuthorization:withData: {#checkAuthZ}

**文件：** AccessEnabler/headers/AccessEnabler.h

**描述：** 应用程序使用此方法检查授权状态。 首先，检查身份验证状态。 如果未通过身份验证，则 [tokenRequestFailed:errorCode:errorDescription:](#tokenReqFailed) 会触发回调，且方法退出。 如果用户已通过身份验证，则还会触发授权流程。 请参阅 [`getAuthorization:`](#getAuthZ) 方法。


<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API调用：检查授权状态</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkAuthorization:(NSString *)resource; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.0+

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API调用：检查授权状态</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) checkAuthorization:(NSString *)resource:
                   withData:(NSDictionary *)data; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.9+

**参数：**

- *资源*:用户请求授权的资源的ID。
- *数据*:包含要发送到付费电视通讯服务的键值对的字典。 Adobe可以使用此数据来启用将来的功能，而无需更改SDK。 

**触发的回调：**
[tokenRequestFailed:errorCode:errorDescription:](#tokenReqFailed)`,setToken:forResource:, sendTrackingData:forEventType:, setAuthenticationStatus:errorCode:`

[回到顶……](#apis)

</br>

### getAuthorization:,getAuthorization:withData: {#getAuthZ}

**文件：** AccessEnabler/headers/AccessEnabler.h

**描述：** 应用程序使用此方法来启动授权流程。 如果用户尚未进行身份验证，则还会启动身份验证流程。 如果用户通过了身份验证， AccessEnabler将继续发出授权令牌（如果本地令牌缓存中不存在有效的授权令牌）和短期媒体令牌的请求。 一旦获得短媒体令牌，则认为授权流程已完成。 的 [setToken:forResource:](#setToken) 触发回调，并将短媒体令牌作为参数交付到应用程序。 如果由于任何原因授权失败， [tokenRequestFailed:forEventType:](#tokenReqFailed) 会触发回调并提供错误代码/详细信息。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API调用：启动授权流程</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthorization:(NSString *)resource; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.0+

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API调用：启动授权流程</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getAuthorization:(NSString *)resource:
                 withData:(NSDictionary *)data; </code></pre></td>
</tr>
</tbody>
</table>

 

**可用性：** v1.9+

**参数：**

- *资源*:用户请求授权的资源的ID。
- *数据*:包含要发送到付费电视通讯服务的键值对的字典。 Adobe可以使用此数据来启用将来的功能，而无需更改SDK。 

**触发的回调：** `tokenRequestFailed:errorCode:errorDescription:, setToken:forResource:,sendTrackingData:forEventType:`

**触发的其他回调：**\
此方法还可以触发以下回调（如果还启动了身份验证流程）： `setAuthenticationStatus:errorCode:`, `displayProviderDialog:`\
 
**注意：请使用checkAuthorization:/ checkAuthorization:withData: 而不是getAuthorization: / getAuthorization:withData: 尽可能。 getAuthorization: / getAuthorization:withData: 方法将启动完整的身份验证流程（如果用户未进行身份验证），这可能导致程序员方的复杂实施。**

[回到顶……](#apis)

</br>

### setToken:forResource: {#setToken}

**文件：** AccessEnabler/headers/EntitlementDelegate.h

**描述** 由AccessEnabler触发的回调，用于通知您的应用程序授权流程已成功完成。 短暂的媒体令牌也作为参数提供。\
 

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回调：授权流程已成功完成</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setToken:(NSString *)token 
      forResource:(NSString *)resource; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.0+

**参数**:

- *令牌*:短暂的媒体令牌
- *资源*:获得授权的资源

**触发者：** [checkAuthorization:](#checkAuthZ)` , `[checkAuthorization:withData:](#checkAuthZ),` `[getAuthorization:](#getAuthZ), [getAuthorization:withData:](#getAuthZ)

[回到顶……](#apis)

</br>

### tokenRequestFailed:errorCode:errorDescription: {#tokenReqFailed}

**文件：** AccessEnabler/headers/EntitlementDelegate.h

**描述** 由AccessEnabler触发的回调通知上层应用程序授权流程失败。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回调：授权流失败</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) tokenRequestFailed:(NSString *)resource 
                  errorCode:(NSString *)code 
           errorDescription:(NSString *)description; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.0+

**参数**:

- *资源*:获得授权的资源。
- *代码*:与失败方案关联的错误代码。 可能值：
   - `USER_NOT_AUTHORIZED_ERROR`  — 用户无法为给定资源授权
- *描述*:有关失败方案的其他详细信息。 如果此描述性字符串因任何原因不可用，则Primetime身份验证会发送一个空字符串 **(&quot;&quot;)**. \
   MVPD可以使用此字符串传递自定义错误消息或与销售相关的消息。 例如，如果某个订阅者被拒绝授权某个资源，则MVPD可以发送消息，例如：“您当前无权访问包中的此渠道。 如果要升级包，请单击 **此处**.&quot; 该消息由Primetime身份验证通过此回调传递给程序员，程序员可以选择显示或忽略该消息。 Primetime身份验证还可以使用此参数提供可能导致错误的条件通知。 例如，“与提供商的授权服务通信时发生网络错误”。

**触发者：** ` checkAuthorization:, `[checkAuthorization:withData:](#checkAuthZ), `getAuthorization:, `[getAuthorization:withData:](#getAuthZ)

[回到顶……](#apis)

</br>

### 注销 {#logout}

**文件：** AccessEnabler/headers/AccessEnabler.h

**描述：** 应用程序将调用此方法以启动注销流程。 注销是一系列HTTP重定向操作的结果，因为用户需要从Primetime身份验证服务器以及MVPD服务器注销。 由于此流程无法通过AccessEnabler库发出的简单HTTP请求来完成，因此， `UIWebView/WKWebView or SFSafariViewController` 控制器需要进行实例化，才能执行HTTP重定向操作。

注销流程与验证流程不同，因为用户不需要与 `UIWebView/WKWebView or SFSafariViewController`  控制者。 因此，Adobe建议您在注销过程中使控件不可见（即隐藏）。

采用与认证流类似的模式。 iOS AccessEnabler会触发 `navigateToUrl:` 回调或 `navigateToUrl:useSVC:` 创建 `UIWebView/WKWebView or SFSafariViewController` 控制器和，以加载回调中提供的URL `url` 参数。 这是后端服务器上注销端点的URL。 对于tvOS AccessEnabler， `navigateToUrl:` 回调或 `navigateToUrl:useSVC:` 调用回调。

在进行多次重定向时，您的应用程序必须监控 `UIWebView/WKWebView or SFSafariViewController `控制器并检测加载特定自定义URL的时间。 请注意，此特定的自定义URL实际上无效，并且不希望控制器实际加载它。 它只能被您的应用程序解释为注销流程已完成并且关闭控制器是安全的信号。 当控制器加载此特定的自定义URL时，您的应用程序必须关闭控制器并调用AccessEnabler的 `handleExternalURL:url `API方法。 如果您的应用程序需要使用 `SFSafariViewController `控制器特定的自定义URL由 `application's custom scheme` (例如，`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com`)，否则，此特定的自定义URL由 `ADOBEPASS_REDIRECT_URL `常量(即 `adobepass://ios.app`)。

最后， AccessEnabler将调用 [`setAuthenticationStatus()`](http://tve.helpdocsonline.com/ios-tvos-api-reference$setAuthNStatus) 状态代码为0的回调，表示注销流程成功。

**注意：** 如果用户使用Apple SSO登录，则将触发VSA203状态。 如果是这种情况，应指示用户也注销系统设置。 如果不这样做，则在应用程序重新启动时，将导致重新验证。


<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API调用：启动注销流程</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) logout; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.0+

**参数：** 无

**触发的回调：** `navigateToUrl:, `[`setAuthenticationStatus:errorCode:`](#setAuthNStatus)

 

[回到顶……](#apis)

</br>

### getSelectedProvider {#getSelProv}

**文件：** AccessEnabler/headers/AccessEnabler.h

**描述：** 使用此方法可确定当前选择的提供程序。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API调用：确定当前选定的MVPD</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getSelectedProvider; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.0+

**参数：** 无

**触发的回调：** [`selectedProvider:`](#selProv)

[回到顶……](#apis)

</br>

### selectedProvider {#selProv}

**文件：** AccessEnabler/headers/EntitlementDelegate.h

**描述** 由AccessEnabler触发的回调，该回调将有关当前选定MVPD的信息传送到应用程序。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回调：有关当前选定MVPD的信息</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) selectedProvider:(MVPD *)mvpd;</code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.0+

**参数**:

- *mvpd*:包含有关当前选定MVPD的信息的对象

**触发者：** [`getSelectedProvider`](#getSelProv)

[回到顶……](#apis)

</br>

### getMetadata: {#getMeta}

**文件：** AccessEnabler/headers/AccessEnabler.h

**描述：** 使用此方法可检索AccessEnabler库作为元数据公开的信息。 应用程序可以通过提供基于字典的数据来访问此数据 *key* 输入参数。

程序员可以使用两种类型的元数据：

- 静态元数据（身份验证令牌TTL、授权令牌TTL和设备ID） 
- 用户元数据(用户特定信息，如用户ID、邮政编码；可以在身份验证和授权流程期间从MVPD传递到用户设备)

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>API调用：查询AccessEnabler以获取元数据</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) getMetadata:(NSDictionary *)keyDictionary; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.0+

**参数：**

- *keyDictionary*:字典数据结构，具有以下格式：
   - 如果键为 `METADATA_OPCODE_KEY` 值为 `METADATA_AUTHENTICATION`，则会进行查询以获取身份验证令牌过期时间。
   - 如果键为 `METADATA_OPCODE_KEY` 值为 `METADATA_AUTHORIZATION` **和**\
      键 `METADATA_RESOURCE_ID_KEY` 并且值是特定的资源ID，则进行查询以获取与指定资源关联的授权令牌的过期时间。
   - 如果键为 `METADATA_OPCODE_KEY` 值为 `METADATA_DEVICE_ID`，然后进行查询以获取当前设备id。 请注意，此功能默认处于禁用状态，程序员应联系Adobe以获取有关启用和费用的信息。
   - 如果键为 `METADATA_OPCODE_KEY` 值为 `METADATA_USER_META` **和** 键 `METADATA_USER_META_KEY` 值是元数据的名称，则会为用户元数据创建查询。 可用用户元数据类型的列表：
      - `zip`  — 邮政编码列表
      - `householdID`  — 家庭标识符。 如果MVPD不支持子帐户，则与 `userID`.
      - `maxRating`  — 用户家长评分上限的集合
      - `userID`  — 用户标识符。 如果MVPD支持子帐户，并且用户不是主帐户， `userID` 将不同于 `householdID.`
      - `channelID`  — 用户有权查看的渠道列表。

   **注意：** 程序员可用的实际用户元数据取决于MVPD提供的内容。  此列表将随新元数据的提供和添加到Primetime身份验证系统中而扩展。

**触发的回调：** [`setMetadataStatus:encrypted:forKey:andArguments:`](#setMetaStatus)

**更多信息：** [用户元数据](https://tve.helpdocsonline.com/user-metadata-v2)

[回到顶……](#apis)

</br>

### presentTVProviderDialog {#presentTvDialog}

**文件：** AccessEnabler/headers/EntitlementDelegate.h

**描述** 调用后由AccessEnabler触发的回调[getAuthentication()](#getAuthN) 如果当前请求者支持至少一个支持SSO的MVPD。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回调：单点登录流程的结果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) presentTvProviderDialog: (UIViewController *) viewController; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v2.0+

**参数**:

- viewController:表示Apple SSO对话框。 此viewController需要显示在屏幕上。

**触发者：** [`getAuthentication`](#getAuthN)

**更多信息：** [iOS/tvOS单点登录](https://tve.helpdocsonline.com/ios-tvos-sdk-api-reference#)

[回到顶……](#apis)

</br>

### discessTVProviderDialog {#dismissTvDialog}

**文件：** AccessEnabler/headers/EntitlementDelegate.h

**描述** 用户关闭Apple SSO对话框后，由AccessEnabler触发的回调。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回调：单点登录流程的结果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) dismissTvProviderDialog: (UIViewController *) viewController; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v2.0+

**参数**:

- viewController:表示Apple SSO对话框。 需要从屏幕中删除此viewController。

**触发者：** 用户操作

**更多信息：** [iOS/tvOS单点登录](https://tve.helpdocsonline.com/ios-tvos-sdk-api-reference#)

 

[回到顶……](#apis)

</br>

### setMetadataStatus:encrypted:forKey:andArguments: {#setMetaStatus}

**文件：** AccessEnabler/headers/EntitlementDelegate.h

**描述** 由AccessEnabler触发的回调，该回调通过 [`getMetadata:`](#getMeta) 呼叫。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回调：元数据检索请求的结果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) setMetadataStatus:(id)metadata
                 encrypted:(bool)encrypted 
                    forKey:(int)key 
              andArguments:(NSDictionary *)arguments; </code></pre></td>
</tr>
</tbody>
</table>

**可用性：** v1.0+

**参数**:

- *元数据*:请求的元数据。 此值是 `NSString` 对于静态元数据（身份验证TTL、授权TTL、设备ID）。  请求用户特定的元数据时，它是一个复杂的对象。 此复杂对象通常是JSON有效负载的Objective-C表示形式(例如，“{”street:“主大道”、“建筑”： [“150”、“320”]}&#39;在Objective-C中被翻译为NSDictionary(&quot;street&quot; -> &quot;Main Avenue&quot;, &quot;boulds&quot; -> NSArray(&quot;150&quot;, &quot;320&quot;))。   元数据JSON对象示例：

```JSON
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
```

- *加密*：指定检索的元数据是否加密的布尔值。 此参数仅对于用户元数据请求而言很重要，对于始终未加密接收的静态元数据（例如，身份验证TTL），此参数没有任何意义。 如果此参数设置为true，则程序员需通过使用白名单私钥(与在 [`setRequestor:setSignedRequestorId:`](#setReq) 和 `setRequestor:setSignedRequestorId:serviceProviders: `调用)。

- *key*:用于构建元数据检索请求的键。

- *参数*:那本字典被传到 [`getMetadata:`](#getMeta) 呼叫。 提供此选项是为了允许应用程序将请求与响应进行匹配。

**触发者：** [`getMetadata:`](#getMeta)

**更多信息：** [用户元数据](https://tve.helpdocsonline.com/user-metadata-v2)


[回到顶……](#apis)

</br>

### MVPD {#mvpd}

**文件：** AccessEnabler/headers/model/MVPD.h

**描述** 描述MVPD对象。 可用于获取有关MVPD属性的信息。

**可用性：** v1.0+ [v2.2中提供了poardingStatus属性] 

**属性**:

- (NSString)ID - MVPD Id。
- (NSString)displayName - MVPD名称。 [此参数应用于在选取器中显示]
- (NSString)logoURL - MVPD徽标地址。
- (BOOL)enablePlatformServices — 如果为true，则MVPD支持SSO服务，例如 [Apple SSO](https://tve.helpdocsonline.com/ios-tvos-sdk-api-reference#).
- (NSString)toardingStatus — 可以有3个值：
   - nil - MVPD不支持Apple SSO。
   - 选取器 — MVPD可显示在Apple选取器中，但验证流程由Adobe完成。
   - 支持 — Apple完全支持MVPD，并将使用Apple的SSO令牌。

[回到顶……](#apis)

</br>

## 跟踪事件 {#tracking}

AccessEnabler会触发一个与授权流不一定相关的额外回调。 实施 [`sendTrackingData()`](#sendTracking) callback函数是可选函数，但它使应用程序能够跟踪特定事件并编译统计信息，如成功/失败的身份验证/授权尝试次数。 

### sendTrackingData:forEventType: {#sendTracking}

**文件：** AccessEnabler/headers/EntitlementDelegate.h

**描述** 由AccessEnabler向应用程序发出信令来触发各种事件（如身份验证/授权流的完成/失败）的回调。 使用Primetime身份验证1.6时，将报告设备类型、AccessEnabler客户端类型和操作系统 [`sendTrackingData()`](#sendTracking). 的 [`sendTrackingData()`](#sendTracking) 回调仍向后兼容。

<table class="pass_api_table">
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>回调：跟踪事件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre><code>- (void) sendTrackingData:(NSArray *)data 
             forEventType:(int)event; </code></pre></td>
</tr>
</tbody>
</table>

 

**可用性：** v1.0+

**注意：** 设备类型和操作系统是通过使用公共Java库(<http://java.net/projects/user-agent-utils>)和用户代理字符串。 请注意，此信息仅作为一种将操作量度划分为设备类别的粗略方式提供，但该Adobe不会对错误结果负责。 请相应地使用新功能。

- 设备类型的可能值：
   - `computer`
   - `tablet`
   - `mobile`
   - `gameconsole`
   - `unknown`

- AccessEnabler客户端类型的可能值：
   - `flash`
   - `html5`
   - `ios`
   - `android`


**参数**:

- *事件*:被跟踪事件的代码。 有三种可能的跟踪事件类型：
   - **authorizationDetection:** 授权令牌请求随时返回(事件为 `TRACKING_AUTHORIZATION`)
   - **authenticationDetection:** 每次进行身份验证检查(事件为 `TRACKING_AUTHENTICATION`)
   - **mvpdSelection:** 当用户在MVPD选择表单中选择MVPD时(事件为 `TRACKING_GET_SELECTED_PROVIDER`)
- *数据*:与所报告事件关联的其他数据。 此数据以值列表的形式显示。

**触发者：** `checkAuthentication, getAuthentication, `[getAuthentication:withData:](#getAuthN), `checkAuthorization:, `[checkAuthorization:withData:](#checkAuthZ), `getAuthorization:, `[getAuthorization:withData:](#getAuthZ), `setSelectedProvider:`

解释 *数据* 数组：

- 对于trackingEventType `TRACKING_AUTHENTICATION:`
   - **0**  — 令牌请求是否成功(true/false)，如果成功：
   - **1** - MVPD ID字符串
   - **2** - GUID（md5哈希）
   - **3**  — 缓存中已有令牌(true/false)
   - **4**  — 设备类型
   - **5** - AccessEnabler客户端类型
   - **6**  — 操作系统类型

- 对于trackingEventType `TRACKING_AUTHORIZATION:`
   - **0**  — 令牌请求是否成功(true/false)，如果成功：
   - **1** - MVPD ID
   - **2** - GUID（md5哈希）
   - **3**  — 缓存中已有令牌(true/false)
   - **4**  — 错误
   - **5**  — 详细信息
   - **6**  — 设备类型
   - **7** - AccessEnabler客户端类型
   - **8**  — 操作系统类型
- 对于trackingEventType `TRACKING_GET_SELECTED_PROVIDER:`
   - **0**  — 当前选定MVPD的ID
   - **1**  — 设备类型
   - **2** - AccessEnabler客户端类型
   - **3**  — 操作系统类型

</br>

## 相关信息 {#related}

- [iOS集成指南](/help/authentication/iostvos-sdk-cookbook.md)
- [iOS技术概述](/help/authentication/iostvos-sdk-overview.md)
- [授权流程](https://tve.helpdocsonline.com/entitlement-flow)
- [在Primetime身份验证中跟踪数据](https://tve.helpdocsonline.com/tracking-data-in-adobe-pass)
