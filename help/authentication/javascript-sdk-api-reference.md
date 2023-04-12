---
title: JavaScript SDK API参考
description: JavaScript SDK API参考
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2835'
ht-degree: 0%

---


# JavaScript SDK API参考 {#javascript-sdk-api-reference}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## API参考 {#api-reference}

这些函数启动与MVPD交互的请求。 所有调用均是异步的；您必须实施 [回调](#callbacks) 要处理响应，请执行以下操作：

- [setRequestor()](#setReq)
- [getAuthorization()](#getAuthZ)
- [getAuthentication()](#getAuthN)
- [checkAuthentication()](#checkAuthN)
- [checkAuthorization()](#checkAuthZ)
- [checkPreauthorizedResources()](#checkPreauthRes)
- [getMetadata()](#getMeta)
- [setSelectedProvider()](#setSelProv)
- [logout()](#logout)


## setRequestor(inRequestorID， endpoints， options){#setrequestor(inRequestorID,endpoints,options)}

**描述：** 标识请求源自的网站。  您必须在通信会话中进行任何其他API调用之前进行此调用。 

**参数：**

- *inRequestorID*  — 在注册期间分配给始发站点的Adobe的唯一标识符。

- *端点*  — 此参数是可选的。 它可以是以下值之一：

   - 一个数组，用于指定由Adobe提供的身份验证和授权服务的端点（可能出于调试目的而使用不同的实例）。 如果提供了多个URL，则MVPD列表由所有服务提供商的端点组成。 每个MVPD都与最快的服务提供商关联；即首先响应并支持该MVPD的提供商。 默认情况下（如果未指定值），将使用Adobe服务提供程序(<http://sp.auth.adobe.com/>)。

   示例：
   - `setRequestor("IFC", ["http://sp.auth-dev.adobe.com/adobe-services"])`


- *选项*  — 包含应用程序ID值、访客ID值无刷设置（后台登录注销）和MVPD设置(iFrame)的JSON对象。 所有值都是可选的。
   1. 如果指定，则将在库执行的所有网络调用中报告Experience CloudvisitorID。 该值稍后可用于高级分析报表。
   2. 如果指定了应用程序的唯一标识符 — `applicationId`  — 该值将作为X-Device-Info HTTP标头的一部分添加到应用程序进行的所有后续调用中。 稍后可以从 [ESM](/help/authentication/entitlement-service-monitoring-overview.md) 报表。

   **注意：** 所有JSON键都区分大小写。

    示例：

```JSON
   setRequestor("IFC", {
      "visitorID": "THE_ECID_VALUE",
      "applicationId": "APP_ID_VALUE"
  })
```

- 程序员可以通过指定是否需要iFrame进行登录(*iFrameRequired* 键)和iFrame尺寸(*iFrameWidth* 和 *iFrameHeight* 键)。 JSON对象具有以下模板：

```JSON
    {  
       "visitorID": <string>,
       "backgroundLogin": <boolean>,
       "backgroundLogout": <boolean>,
       "mvpdConfig":{  
          "MVPD_ID_1":{  
             "iFrameRequired": <boolean>,
             "iFrameWidth": <integer>,
             "iFrameHeight": <integer>
          },
          ...
          "MVPD_ID_N":{  
             "iFrameRequired": <boolean>,
             "iFrameWidth": <integer>,
             "iFrameHeight": <integer>
          }
       }
    }
```
 

上述模板中的所有顶级键都是可选的，并且具有默认值(*backgroundLogin*, *backgroundLogut*&#x200B;默认为false，而mvpdConfig为null — 表示不覆盖MVPD设置)。

 
- **注意**:为上述参数指定无效值/类型将导致行为未定义。

 

以下是以下方案的配置示例：激活无刷新登录和注销，将MVPD1更改为全页重定向登录（非iFrame），将MVPD2更改为iFrame登录，宽度=500，高度=300:

```JSON
    {  
       "backgroundLogin": true,
       "backgroundLogout": true,
       "mvpdConfig":{  
          "MVPD1":{  
             "iFrameRequired": false
          },
          "MVPD2":{  
             "iFrameRequired": true,
             "iFrameWidth": 500,
             "iFrameHeight": 300
          }
       }
    }
```


**触发的回调：** [setConfig()](#setconfigconfigxml-setconfigconfigxml)
</br>

[返回页首](#top)

</br>

## getAuthorization(inResourceID， redirect_url) {#getauthorization(inresourceid,redirect_url)}

**描述：** 请求对指定资源的授权。 每当客户尝试访问可授权的资源时，请调用此函数以从Access Enabler中获取短时的授权令牌。 资源ID与提供授权的MVPD协议。

为当前客户使用缓存的身份验证令牌。 如果未找到此类令牌，请先启动身份验证过程，然后继续授权。\
 
**参数：**

- `inResourceID`  — 用户请求授权的资源的ID。
- `redirect_url`  — 可选地提供重定向URL，以便MVPD的授权过程将用户返回到该页面，而不是从中启动授权的页面。


**触发的回调：** [setToken()](#settokeninrequestedresourceid-intoken-settokeninrequestedresourceidintoken) 成功时， [tokenRequestFailed](#tokenrequestfailedinrequestedresourceid-inrequesterrorcode-inrequestdetailederrormessage-tokenrequestfailedinrequestedresourceidinrequesterrorcodeinrequestdetailederrormessage) 失败

>[!CAUTION]
>
>请尽可能使用checkAuthorization()而不是getAuthorization()。 getAuthorization()方法将启动完整的身份验证流程（如果用户未进行身份验证），这可能导致程序员方面实施复杂。

</b>

[返回页首](#top)

</br>

## getAuthentication(redirect_url) {#getauthentication(redirect_url}

**描述：** 请求当前客户的身份验证。 通常在单击“登录”按钮时调用。 检查当前客户的缓存身份验证令牌。 如果未找到此类令牌，则启动身份验证过程。 这会调用默认或自定义提供程序选择对话框，然后使用选定的提供程序重定向到MVPD的登录界面。

成功时，为用户创建并存储身份验证令牌。 如果身份验证失败，提供程序会向 [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode) 回调。

**参数：**

- redirect_url — （可选）提供一个重定向URL，以便MVPD的身份验证过程会将用户返回到该页面，而不是从中启动身份验证的页面。

 **触发的回调：** [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode), [displayProviderDialog()](#displayproviderdialogproviders-displayproviderdialogproviders), [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata)

</br>

[返回页首](#top)

</br>

## checkAuthN {#checkauthn}

**描述：** 检查当前客户的当前身份验证状态。  未与任何UI关联。

**触发的回调：** [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode)

</br>

[返回页首](#top)

</br>

## checkAuthorization(inResourceID) {#checkauthorization(inresourceid)}

**描述：** 应用程序使用此方法检查当前客户和给定资源的授权状态。 首先，检查身份验证状态。 如果未通过身份验证，则会触发tokenRequestFailed()回调，并且方法将退出。 如果用户已通过身份验证，则还会触发授权流程。 请参阅 [getAuthorization()](#getAuthZ方法。

>[!TIP]
>
> **使用check-status函数**  在请求授权之前，您无需检查身份验证或授权的状态。 例如，您可以调用这些函数来更新您自己的状态显示。 当您需要任何用户交互时，请勿使用它们。

**参数：**

- `inResourceID`  — 用户请求授权的资源的ID。

 
**触发的回调：**
[setToken()](#settokeninrequestedresourceid-intoken-settokeninrequestedresourceidintoken), [tokenRequestFailed()](#tokenrequestfailedinrequestedresourceid-inrequesterrorcode-inrequestdetailederrormessage-tokenrequestfailedinrequestedresourceidinrequesterrorcodeinrequestdetailederrormessage), [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata), [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode)

</br>

## checkPreauthorizedResources(resources) {#checkPreauthorizedResources(resources)}

**描述：** 请求“预检”授权状态以获取资源列表。

**参数：**

- *资源*:资源参数是应检查授权的资源数组。 列表中的每个元素都应是一个表示资源ID的字符串。 资源ID受与 `getAuthorization()` 调用，即程序员与MVPD或媒体RSS片段之间建立的约定值。 

</br>

## checkPreauthorizedResources(resources-cache=true) {#checkPreauthorizedResources(resources-cache=true)}

从JS SDK版本4.0开始，提供了此API变体


**参数：**

- *资源*:资源参数是应检查授权的资源数组。 列表中的每个元素都应是一个表示资源ID的字符串。 资源ID受与 `getAuthorization()` 调用，即程序员与MVPD或媒体RSS片段之间建立的约定值。 

- *缓存*:检查预授权资源时是否使用内部缓存。 这是一个可选参数，默认为 **true**. 如果为true，则行为与上述API相同，这意味着后续调用此函数时将使用内部缓存来解析预授权资源。 传递 **false** 对于此参数，将禁用内部缓存，每次在 **checkPreauthorizedResources** 调用API。

**触发的回调：** [preauthorizedResources()](#preauthorizedresourcesauthorizedresources-preauthorizedresourcesauthorizedresources)
 
</br>

[返回页首](#top)
</br>

## getMetadata(Key) {#getMetadata}

**描述：** 检索作为元数据由Access Enabler库公开的信息。

元数据有两种类型： 

- **静态** （身份验证令牌TTL、授权令牌TTL和设备ID） 
- **用户元数据** （这包括在身份验证和/或授权流程期间从MVPD传递到用户设备的用户特定信息）

**更多信息：** [用户元数据](#UserMetadata)

**参数：**

- *key*:用于指定所请求元数据的ID:
   - 如果键为 `"TTL_AUTHN",` 然后，进行查询以获取身份验证令牌过期时间。

   - 如果键为 `"TTL_AUTHZ"` 而params是一个将资源id作为字符串包含在内的数组，则会进行查询以获取与指定资源关联的授权令牌的过期时间。

   - 如果键为 `"DEVICEID"` 然后，进行查询以获取当前设备id。 请注意，此功能默认处于禁用状态，程序员应联系Adobe以获取有关启用和费用的信息。

   - 如果键来自以下用户元数据类型列表，则会将包含相应用户元数据的JSON对象发送到 [`setMetadataStatus()`](#setmetadatastatuskey-encrypted-data-setmetadatastatuskeyencrypteddata) 回调函数：

   - `"zip"`  — 邮政编码

   - `"encryptedZip"`  — 加密的邮政编码

   - `"householdID"`  — 家庭标识符。 如果MVPD不支持子帐户，则此ID将与userID相同。

   - `"maxRating"`  — 用户的家长评分上限

   - `"userID"`  — 用户标识符。 如果MVPD支持子帐户，而用户不是主帐户，则userID将与houselID不同。

   - `"channelID"`  — 用户有权查看的渠道列表

   - `"is_hoh"`  — 标识用户是否为户主的标记

   - `"encryptedZip"`  — 加密的邮政编码

   - `"typeID"`  — 标识用户帐户是主/次帐户的标记

   - `"primaryOID"`  — 家庭标识符

   - `"postalCode"`  — 类似于邮政编码

   - `"acctID"`  — 帐户ID

   - `"acctParentID"`  — 帐户父ID
   **注意**:程序员可用的实际用户元数据取决于MVPD提供的内容。  请参阅 [用户元数据](#UserMetadata) ，用于当前可用用户元数据列表。


例如：

```JSON
    // Assume that a reference to the AccessEnabler has been previously 
    // obtained and stored in the "ae" variable
     
    ae.setRequestor("SITE");
    ae.checkAuthentication();
     
    function setAuthenticationStatus(status, reason) {
        if (status ==  1) {
            //user is authenticated, request metadata
            ae.getMetadata("zip");
            ae.getMetadata("maxRating");
        } else {
            ...
      }
    }
```
 

**触发的回调：** [setMetadataStatus()](#setmetadatastatuskey-encrypted-data-setmetadatastatuskeyencrypteddata)

</br>

[返回页首](#top)

</br>


## setSelectedProvider(providerid) {#setSelectedProvider}

**描述：** 当用户从提供商选择UI中选择了MVPD以将提供商选择发送到访问启用程序时，请调用此函数，或者使用空参数调用此函数，以防用户在没有选择提供商的情况下取消提供商选择UI。 

**触发的回调：**[ setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode), [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata)

</br>

[返回页首](#top)

</br>

## getSelectedProvider() {#getSelectedProvider}

**描述：** 在提供程序选择对话框中检索客户选择的结果。 在进行初始身份验证检查后，可随时使用此功能。

此函数是异步的，并将其结果返回给 `selectedProvider()` 回调函数。

- **MVPD** 当前选择的MVPD，或者如果未选择MVPD，则为空。
- **AE_State** 当前客户的身份验证结果为“新用户”、“用户未验证”或“用户已验证”

 **触发的回调：** [selectedProvider()](#getselectedprovider-getselectedprovider)

</br>

[返回页首](#top)

</br>

## 注销 {#logout}

**描述：** 注销当前客户，清除该用户的所有身份验证和授权信息。 从客户的系统中删除所有authN和authZ令牌。

 **触发的回调：** [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode)
</br> 

[返回页首](#top)

</br>

## 回调定义 {#calllback-definitions}

您必须实施这些回调来处理对异步请求调用的响应：

- [entitlementLoaded()](#entitlementloaded-entitlementloaded)
- [setConfig()](#setconfigconfigxml-setconfigconfigxml)
- [displayProviderDialog()](#displayproviderdialogproviders-displayproviderdialogproviders)
- [createIFrame()](#createiframe-createiframeinwidthminheight)
- [setAuthenticationStatus()](#setauthenticationstatusisauthenticated-errorcode)
- [sendTrackingData()](#sendtrackingdatatrackingeventtype-trackingdata-sendtrackingdatatrackingeventtypetrackingdata)
- [setToken()](#settokeninrequestedresourceid-intoken-settokeninrequestedresourceidintoken)
- [tokenRequestFailed()](#tokenrequestfailedinrequestedresourceid-inrequesterrorcode-inrequestdetailederrormessage-tokenrequestfailedinrequestedresourceidinrequesterrorcodeinrequestdetailederrormessage)
- [preauthorizedResources()](#preauthorizedresourcesauthorizedresources-preauthorizedresourcesauthorizedresources)
- [setMetadataStatus()](#setmetadatastatuskey-encrypted-data-setmetadatastatuskeyencrypteddata)
- [selectedProvider()](#selectedproviderresult-selectedprovider)

</br>

## entitlementLoaded() {#entitlementLoaded}

**描述：** 当Access Enabler完成初始化并准备接收请求时触发。 实施此回调以了解何时可以开始与Access Enabler API通信。
</br>

[返回页首](#top)

</br>

## setConfig(configXML) {#setconfig(configXML)}

**描述：** 实施此回调以接收配置信息和MVPD列表。

**参数：**

- *configXML*:xml对象，其中包含当前请求者（包括MVPD列表）的配置。

 
**触发者：** [setRequestor()](#setrequestor-inrequestorid-endpoints-optionssetreq)

</br>

[返回页首](#top)

</br>

## displayProviderDialog(providers) {#displayproviderdialog(providers)}

**描述：** 实施此回调以调用您自己的自定义提供程序选择UI。 您的对话框应使用显示名称（和可选徽标）来提供客户的选择。 当客户做出选择并取消对话框时，在对 *setSelectedProvider()*.

**参数：**

- *提供商*  — 表示请求的MVPD的对象数组：

```JSON
    var mvpd = {
        ID: "someprov",
        displayName: "Some Provider",
        logoURL: "http://www.someprov.com/images/logo.jpg"
    }
```

**触发者：** [getAuthentication()](#getauthenticationredirecturl-getauthenticationredirecturl), [getAuthorization()](#getauthorizationinresourceid-redirecturl-getauthorizationinresourceidredirecturl)

</br>[返回页首](#top)

</br>

## createIFrame(inWidth， inHeight) {#createIFrame(inWidth,inHeight)}

**描述：** 如果用户选择的MVPD要求iFrame在其中显示其身份验证登录页面UI，则实施此回调。

**触发者：**[ setSelectedProvider()](#setselectedproviderproviderid-setselectedprovider)

</br> [返回页首](#top)

</br>

## setAuthenticationStatus(isAuthenticated， errorCode) {#set-authn-status-isauthn-error}

**描述：** 实施此回调以接收身份验证状态（1=authenticated或0=not authenticated），以及在尝试确定身份验证状态时发生任何错误（成功完成检查时出现空字符串）时的描述性错误消息。

>[!NOTE]
> 
>如果您使用的是当前版本， [提前错误报告](/help/authentication/error-reporting.md) 系统中，可以忽略发送到此函数的errorCode参数。  但是，isAuthenticated标记仍可用于跟踪授权流程中用户的身份验证状态


**参数：**

- *isAuthenticated*  — 提供身份验证状态：1（已验证）或0（未验证）。
- *errorCode*  — 确定身份验证状态时发生的任何错误。 空字符串（如果没有）。

 
**触发者：** [checkAuthentication()](#checkauthn-checkauthn), [getAuthentication()](#getauthenticationredirecturl-getauthenticationredirecturl), [checkAuthorization()](#checkauthorizationinresourceid-checkauthorizationinresourceid)

</br>

[返回页首](#top)

</br>

## sendTrackingData(trackingEventType， trackingData) {#sendTrackingData(trackingEventType,trackingData)}

>[!CAUTION]
>
>设备类型和操作系统是通过使用公共Java库(<http://java.net/projects/user-agent-utils>)和用户代理字符串。 请注意，此信息仅作为一种将操作量度划分为设备类别的粗略方式提供，但该Adobe不会对错误结果负责。 请相应地使用新功能。

**描述：** 实施此回调以在发生特定事件时接收跟踪数据。 例如，您可以使用此功能来跟踪有多少用户使用相同的凭据登录。 当前无法配置跟踪。 使用Adobe Primetime身份验证1.6, `sendTrackingData()` 还报告有关设备、Access Enabler客户端和操作系统类型的信息。 的 `sendTrackingData()` 回调仍向后兼容。\
 
- 设备类型的可能值：
   - 计算机
   - 平板电脑
   - 移动设备
   - 游戏机
   - 未知

- Access Enabler客户端类型的可能值：
   - html5
   - ios
   - android


传递事件类型和关联信息数组。 事件类型包括：

| mvpdSelection | 用户在提供商选择对话框中选择了MVPD。 |
| ----------------------- | --------------------------------------------------------- |
| authenticationDetection | 验证检查已完成。 |
| authorizationDetection | 授权请求已完成。 |

</br>
数据特定于每个事件类型：
</br>

| 事件类型（字符串） | 数据（数组） |
|:--- | :--- |
| mvpdSelection | 0:选定的MVPD |
|  | 1:设备类型 |
|  | 2:Access Enabler客户端类型 |
|  | 3:操作系统 |
| authenticationDetection | 0:令牌请求是否成功(true/false) |
|  | 1:MVPD ID |
|  | 2:GUID |
|  | 3:缓存中已有令牌(true/false) |
|  | 4:设备类型 |
|  | 5:Access Enabler客户端类型 |
|  | 6:操作系统 |
| authorizationDetection | 0:令牌请求是否成功(true/false) |
|  | 1:MVPD ID |
|  | 2:GUID |
|  | 3:缓存中已有令牌(true/false) |
|  | 4:错误 |
|  | 5:详细信息 |
|  | 6:设备类型 |
|  | 7:Access Enabler客户端类型 |
|  | 8:操作系统 |


**触发者：** [checkAuthentication()](#checkauthn-checkauthn), [getAuthentication()](#getauthenticationredirecturl-getauthenticationredirecturl), [checkAuthorization()](#checkauthorizationinresourceid-checkauthorizationinresourceid), [getAuthorization()](#getauthorizationinresourceid-redirecturl-getauthorizationinresourceidredirecturl)

</br>

[返回页首](#top)

</br>

## setToken(inRequestedResourceID， inToken) {#setToken(inRequestedResourceID,inToken)}

**描述：** 实施此回调以接收已针对其发出授权请求或检查授权请求并成功完成的资源(inRequestedResourceID)的短生命周期媒体令牌(inToken)和ID。

**触发者：** [checkAuthorization()](#checkAuthZ), [getAuthorization()](#getAuthZ)
</br>

[返回页首](#top)

</br>

## tokenRequestFailed(inRequestedResourceID， inRequestErrorCode， inRequestDetailedErrorMessage) {#token-request-failed-error-msg}

**描述：** 实施此回调，以在授权或检查授权请求失败时发出信号。 MVPD可以选择使用来提供程序员要显示的自定义消息。

>[!IMPORTANT]
>
>此回调函数是旧版Primetime身份验证错误报告系统的一部分。 它会保留以进行向后兼容性，但是如果您已使用当前的高级错误报告系统实施了自己的回调，则根本不需要使用此函数。 较新的错误报告系统提供了有关授权（或其他操作）失败原因的更详细信息，以及针对每种错误或警告类型的建议操作过程。

**参数：**

- *inRequestedResourceID*  — 提供授权请求中使用的资源ID的字符串。
- *inRequestErrorCode*  — 显示Adobe Primetime身份验证错误代码的字符串，用于指示失败的原因；可能的值为“用户未验证错误”和“用户未授权错误”；有关更多详细信息，请参阅下面的“回调错误代码”。
- *inRequestDetailedErrorMessage*  — 适用于显示的附加描述性字符串。 如果此描述性字符串因任何原因不可用，则Adobe Primetime身份验证会发送一个空字符串 **(&quot;&quot;)**.  MVPD可以使用此功能传递自定义错误消息或与销售相关的消息。 例如，如果某个订阅者被拒绝授权某个资源，则MVPD可以通过 `*inRequestDetailedErrorMessage*` 例如： **“您当前无权访问包中的此渠道。 如果要升级包，请单击\*此处\*。”** 该消息由Adobe Primetime身份验证通过此回调传递到程序员网站。 然后程序员可以选择显示或忽略它。 Adobe Primetime身份验证也可以使用 `*inRequestDetailedErrorMessage*` 通知程序员可能导致错误的条件。 例如， **“与提供商的授权服务通信时出现网络错误”。**

 

**触发者：**  [checkAuthorization()](#checkauthorizationinresourceid-checkauthorizationinresourceid), [getAuthorization()](#getauthorizationinresourceid-redirecturl-getauthorizationinresourceidredirecturl)
</br>

[返回页首](#top)

</br>


## preauthorizedResources(authorizedResources) {#preauthorizedResources(authorizedResources)}

**描述：** 由Access Enabler触发的回调，该Access Enabler可传送在调用 `checkPreauthorizedResources()`.

**参数：**

- *authorizedResources*：已授权资源的列表。

**触发者：** [checkPreauthorizedResources()](#checkPreauthRes)
</br>

[返回页首](#top)

</br>

## setMetadataStatus(key， encrypted， data) {#setMetadataStatus(key,encrypted,data)}

**描述：** 由Access Enabler触发的回调，该回调通过 `getMetadata()` 呼叫。

**更多信息：** [用户元数据](#userMetadata)

**参数：**

- *键（字符串）*:请求所针对的元数据的键。
- *已加密（布尔值）*:表示是否加密了“value”的标记。 如果为“true”，则“value”实际上将是实际值的JSON Web加密表示形式。 
- *数据（JSON对象）*:表示元数据的JSON对象。对于简单请求(`TTL_AUTHN`&#39;, &#39;`TTL_AUTHZ`&#39;, &#39;`DEVICEID`&#39;)，则结果为字符串（表示身份验证TTL、授权TTL或设备ID）。 对于用户元数据请求，结果可以是表示元数据有效负载的基元对象或JSON对象。 JSON用户元数据对象的实际结构类似于以下内容：

```JSON
    {
        updated: 1334243471,
        encrypted: ["encryptedProp"],
        data: {
            zip: ["12345", "34567"],
            maxrating: { 
                "MPAA": "PG-13",
                "VCHIP": "TV-Y", 
                "URL": "http://exam.pl/e/manage/ratings"
            },
            householdid: "3456",
            uid: "BgSdasfsdk23/dsaf3+saASesadgfsShggssd=",
            channelID: ["channel-1", "channel-2"]
    }
```
 

例如：

```JSON
    // Implement the setMetadataStatus() callback
    function setMetadataStatus(key, encrypted, data) {
        if (encrypted) {
            //the metadata value is encrypted
            //needs to be decrypted by the programmer
            data = decrypt(data);
        }
        alert(key + "=" + data);
    }
```
 

**触发者：** [`getMetadata()`](#getmetadatakey-getmetadata)
</br>
[返回页首](#top)

</br>

## selectedProvider(result) {#selectedProvider(result)}

**描述：** 实施此回调以接收当前选定的MVPD以及封装在 `result` 参数。 的 `result` 参数是具有以下属性的对象：

- **MVPD** 当前选择的MVPD，或者如果未选择MVPD，则为空。
- **AE\_State** 当前用户（“新用户”、“用户未经身份验证”或“用户已验证”中的一个）的身份验证结果

 **触发者：** [getSelectedProvider()](#getSelProv)

</br>

[返回页首](#top)

</br>

### 回调错误代码 {#callback-error-codes}

| 一般错误 |  |
|:--- | :--- | 
| 内部错误 | 尝试处理请求时发生系统错误。 |
| 未选择提供程序错误 | 在提供商选择对话框中客户取消时发生 |
| 提供程序不可用错误 | 在没有提供程序时发生。 |

| 身份验证错误 |  |
|:--- | :--- | 
| 一般身份验证错误 | 原因未知或无法发布时返回。 |
| 内部身份验证错误 | 尝试验证时出现系统错误。 |
| 用户未验证错误 | 用户未通过身份验证。 |
| 多个身份验证请求错误 | 在第一个验证请求完成之前，已收到其他验证请求。 |

| 授权错误 |  |
|:--- | :--- | 
| 一般授权错误 | 原因未知或无法发布时返回。 |
| 内部授权错误 | 尝试授权时出现系统错误。 |
| 用户未授权错误 | 客户无权查看请求的内容。 |

<!--

### Related Information {#Related-Infornation}

* [JavaScript SDK Overview](/help/authentication/javascript-sdk-overview.md)
* [JavaScript SDK Cookbook](/help/authentication/javascript-sdk-cookbook.md)
* **JavaScript Code Samples**
* [Error Reporting](/help/authentication/error-reporting.md)
* [Understanding Tokens](#understanding_tokens)
* **Tracking Data in Adobe Primetime authentication**
-->

[返回页首](#top)

