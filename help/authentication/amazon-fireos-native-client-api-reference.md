---
title: Amazon FireOS Native Client API参考
description: Amazon FireOS Native Client API参考
exl-id: 8ac9f976-fd6b-4b19-a80d-49bfe57134b5
source-git-commit: 84a16ce775a0aab96ad954997c008b5265e69283
workflow-type: tm+mt
source-wordcount: '3416'
ht-degree: 0%

---

# Amazon FireOS Native Client API参考 {#amazon-fireos-native-client-api-reference}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权使用。

</br>

## 介绍 {#intro}

本文档详细介绍Amazon FireOS SDK为Adobe Primetime身份验证公开的方法和回调，Adobe Primetime身份验证支持这些方法和回调。</span> 此处介绍的方法和回调函数在AccessEnabler.h和EntitlementDelegate.h头文件中定义。

请参阅 <https://tve.zendesk.com/hc/en-us/articles/115005561623-fire-TV-Native-AccessEnabler-Library> 获取最新的Amazon FireOS AccessEnabler SDK。

**注意：** Adobe Primetime身份验证团队建议您仅使用Adobe Primetime身份验证 *公共* API：

- 公共API可用 *经过全面测试* 所有受支持的客户端类型。 对于任何公共功能，我们确保每种客户端类型都有相关方法的相应版本。
- 公共API需要尽可能保持稳定，以支持向后兼容性并确保合作伙伴集成不会中断。 但是，对于 *非*-public API，我们保留在以后任何时候更改其签名的权利。 如果您遇到无法通过当前公共Adobe Primetime身份验证API调用组合支持的特定流程，最好的方法是告知我们。 根据您的需求，我们可以修改公共API，并在以后提供稳定的解决方案。

## Amazon FireOS SDK API {#api}

- [getInstance](#getInstance)
- [setOptions](#fire_setOption)
- [setRequestor](#setRequestor)
- [setRequestorComplete](#setRequestorComplete)
- [checkAuthentication](#checkAuthN)
- [getAuthentication](#getAuthN)
- [displayProviderDialog](#displayProviderDialog)
- [setSelectedProvider](#setSelectedProvider)
- [navigateToUrl](#navigagteToUrl)
- [getAuthenticationToken](#getAuthNToken)
- [setAuthenticationStatus](#setAuthNStatus)
- [checkPreauthorizedResources](#checkPreauth)
- [preauthorizedResources](#preauthResources)
- [checkAuthorization](#checkAuthZ)
- [getAuthorization](#getAuthZ)
- [setToken](#setToken)
- [tokenRequestFailed](#tokenRequestFailed)
- [注销](#logout)
- [getselectedprovider](#getSelectedProvider)
- [selectedprovider](#selectedProvider)
- [getMetadata](#getMetadata)
- [setmetadatastatus](#setMetadaStatus)
- [getVersion](#getVersion)

</br>

### Factory.getInstance {#getInstance}

**描述：** 实例化访问启用程序对象。 每个应用程序实例应有一个访问启用程序实例。

| API调用：构造函数 |
| --- |
| ```public static AccessEnabler getInstance(Context appContext, String softwareStatement, String redirectUrl)<br>        throws AccessEnablerException```<br><br> |
| ```public static AccessEnabler getInstance(Context appContext, String env_url, String softwareStatement, String redirectUrl) throws AccessEnablerException``` |

**可用性：** v3.0+


**参数：**

- *appContext*：Amazon Fire OS应用程序上下文。
- softwarestatement
- redirectUrl ：如果是FireOS，则会忽略参数值并将其设置为默认值： adobepass://android.app
- env_url：对于使用Adobe暂存环境进行测试，可以将env\_url设置为“sp.auth-staging.adobe.com”

**已弃用：**

```java
    public static AccessEnabler getInstance(Context appContext)
        throws AccessEnablerException
```


### setRequestor {#setRequestor}

**描述：** 确定程序员的身份。 在为Adobe Primetime身份验证系统注册Adobe时，每个程序员都会分配一个唯一的ID。 在应用程序的生命周期中，只应执行一次此设置。

服务器响应包含MVPD列表以及附加到程序员标识的一些配置信息。 服务器响应由访问启用码在内部使用。 通过setRequestorComplete()回调只向应用程序显示操作的状态（即SUCCESS/FAIL）。

如果 *url* 未使用参数，生成的网络调用将定向默认服务提供商URL：Adobe版本/生产环境。

如果为提供了值， *url* 参数，则生成的网络调用将定向于 *url* 参数。 所有配置请求都在单独的线程中同时触发。 在编译MVPD列表时，优先使用第一个响应程序。 对于列表中的每个MVPD， Access Enabler记住关联服务提供商的URL。 所有后续权利请求都定向到与服务提供程序相关联的URL，该URL在配置阶段与目标MVPD配对。

| API调用：请求者配置 |
| --- |
| ```public void setRequestor(String requestorId)``` |


**可用性：**v 3.0+


| API调用：请求者配置 |
| --- |
| ```public void setRequestor(String requestorId, ArrayList<String> urls)``` |

**可用性：** v3.0+


**参数：**

- *请求者ID*：与程序员关联的唯一ID。 首次向Adobe Primetime身份验证服务注册时，将Adobe分配的唯一ID传递到您的网站。
- *url*：可选参数；默认情况下，使用Adobe服务提供程序(http://sp.auth.adobe.com/)。 此阵列允许您为Adobe提供的身份验证和授权服务指定端点（其他实例可能用于调试目的）。 您可以使用此项指定多个Adobe Primetime身份验证服务提供程序实例。 这样做时，MVPD列表由来自所有服务提供商的端点组成。 每个MVPD都与最快的服务提供程序相关联；即首先响应并支持该MVPD的服务提供程序。

**触发的回调：** `setRequestorComplete()`



**已弃用：**

```
    public void setRequestor(String requestorId, String signedRequestorId)

    public void setRequestor(String requestorId, String signedRequestorId, ArrayList<String> urls)
```

</br>


### setRequestorComplete {#setRequestorComplete}

**描述：** 由Access Enabler触发的回调，通知应用程序配置阶段已完成。 这是一个信号，表明应用程序可以开始发出授权请求。 在配置阶段完成之前，应用程序无法发出任何授权请求。

| 回调：请求者配置完成 |
| --- |
| ```public void setRequestorComplete(int status)``` |

**可用性：** v1.0+

**参数：**

- *状态*：可以采用以下值之一：
   - `AccessEnabler.ACCESS_ENABLER_STATUS_SUCCESS`  — 配置阶段已成功完成
   - `AccessEnabler.ACCESS_ENABLER_STATUS_ERROR`  — 配置阶段失败

**触发者：** `setRequestor()`

</br>


### setOptions {#fire_setOption}

**描述：** 配置全局SDK选项。 它接受 **映射\&lt;string string=&quot;&quot;>** 作为论据。 映射中的值将与SDK发出的每个网络调用一起传递到服务器。

这些值将传递到服务器，与当前流（身份验证/授权）无关。 如果要更改值，可以随时调用此方法。



| API调用： setOptions |
| --- |
| ```public void setOptions(HashMap<String,String> options)``` |

**可用性：** v3.0+

**参数：**

- *options*：地图\&lt;string string=&quot;&quot;> 包含全局SDK选项。 当前提供以下选项：
   - **applicationprofile**  — 可用于根据此值进行服务器配置。
   - **ap\_vi** - visitorIDMarketing Cloud。 此值以后可用于高级分析报表。
   - **device\_info**  — 设备信息，如中所述 **传递设备信息指南**

</br>

### checkAuthentication {#checkAuthN}

**描述：** 检查身份验证状态。 它通过在本地令牌存储空间中搜索有效的身份验证令牌来完成此操作。 调用此方法不会执行任何网络调用。 应用程序使用它来查询用户的身份验证状态并相应地更新UI（即更新登录/注销UI）。 身份验证状态通过 [*setAuthenticationStatus()*](#setAuthNStatus) 回调。

如果MVPD支持“每个请求者的身份验证”功能，则可以在设备上存储多个身份验证令牌。

| API调用：检查身份验证状态 |
| --- |
| ```public void checkAuthentication()``` |

**可用性：** v1.0+

**参数：** 无

**触发的回调：** `setAuthenticationStatus()`

</br>

### getAuthentication {#getAuthN}

**描述：** 启动完整的身份验证工作流。 首先检查身份验证状态。 如果尚未经过身份验证，则身份验证流状态 — 计算机将启动：

- 如果上次验证尝试成功，则会跳过MVPD选择阶段，并且WebView控件将为用户显示MVPD的登录页。
- 如果上次验证尝试不成功，或者用户明确注销，则 [*displayProviderDialog()*](#displayProviderDialog) 会触发回调。 您的应用程序使用此回调来显示MVPD选择UI。 此外，您的应用程序需要通过通知Access Enabler库有关用户的MVPD选择，来恢复身份验证流程。 [setSelectedProvider()](#setSelectedProvider) 方法。

如果MVPD支持“每个请求者的身份验证”功能，则可以在设备上存储多个身份验证令牌（每个程序员一个）。

最后，验证状态通过 *setAuthenticationStatus()* 回调。

| API调用：启动身份验证流程 |
| --- |
| ```public void getAuthentication()``` |

**可用性：** v1.0+

| API调用：启动身份验证流程 |
| --- |
| ```public void getAuthentication(boolean forceAuthN, Map<String, Object> genericData)``` |

**可用性：** v1.0+

**参数：**

- *forceAuthn*：指定是否应启动身份验证流程的标记，无论用户是否已进行身份验证。
- *数据*：包含要发送到Pay-TV pass服务的键值对的映射。 Adobe可以使用此数据启用未来的功能，而无需更改SDK。

**触发的回调：** `setAuthenticationStatus(), displayProviderDialog(), sendTrackingData()`

</br>

### displayProviderDialog {#displayProviderDialog}

**描述** 由Access Enabler触发的回调，用于通知应用程序需要实例化适当的UI元素以允许用户选择所需的MVPD。 回调会提供MVPD对象的列表以及其他有助于正确构建选择UI面板的信息（例如指向MVPD徽标的URL、友好显示名称等）

一旦用户选择了所需的MVPD，则上层应用程序需要通过调用来恢复验证流 *setSelectedProvider()* 并向其传递与用户选择相对应的MVPD的ID。


| **回调：显示MVPD选择UI** |
| --- |
| ```public void displayProviderDialog(ArrayList<Mvpd> mvpds)``` |

**可用性：** v1.0+

**参数**：

- *mvpds*：MVPD对象列表，其中包含应用程序可用于构建MVPD选择UI元素的MVPD相关信息。

**触发者：** `getAuthentication(), getAuthorization()`

</br>

### setSelectedProvider {#setSelectedProvider}

**描述：** 您的应用程序调用此方法以告知访问启用程序用户的MVPD选择。 传递时 *null* 作为参数，Access Enabler将当前MVPD重置为空值。

| **API调用：设置当前选定的提供程序** |
| --- |
| ```public void setSelectedProvider(String mvpdId)``` |


**可用性：**v 1.0+

**参数：** 无

**触发的回调：** `setAuthenticationStatus(), sendTrackingData()`
</br>

### navigateToUrl {#navigagteToUrl}

**描述：** Android SDK上的Access Enabler触发的回调。 在Amazon FireOS SDK中应忽略该错误。

| **“回调：显示MVPD登录”页** |
| --- |
| ```public void navigateToUrl(String url)``` |

**可用性：** v1.0+

**参数：**

- *url*：指向MVPD登录页面的URL

**触发者：** `getAuthentication(), setSelectedProvider()`

</br>

### getAuthenticationToken {#getAuthNToken}

**描述：** 通过从后端服务器请求身份验证令牌来完成身份验证流程。

| **API调用：检索身份验证令牌** |
| --- |
| ```public void getAuthenticationToken(String cookies)``` |

**可用性：** v1.0+

**参数：**

- *Cookie*：在Target域中设置的Cookie（请参阅SDK中的演示应用程序以了解参考实施）。

**触发的回调：** `setAuthenticationStatus(), sendTrackingData()`

</br>

### setAuthenticationStatus {#setAuthNStatus}

**描述：** 由Access Enabler触发的回调，通知应用程序身份验证的状态。 在许多地方，身份验证流程可能会由于用户交互或其他不可预见的情况（如网络连接问题等）而失败。 此回调会通知应用程序身份验证的成功/失败状态，同时还会在需要时提供有关失败原因的其他信息。

此回调也会在注销流完成时发出信号。

| **回调：报告身份验证流的状态** |
| --- |
| ```public void setAuthenticationStatus(int status, String errorCode)``` |

**可用性：** v1.0+

**参数：**

- *状态*：可以采用以下值之一：
   - `AccessEnabler.ACCESS_ENABLER_STATUS_SUCCESS`  — 身份验证流程已成功完成
   - `AccessEnabler.ACCESS_ENABLER_STATUS_ERROR`  — 身份验证流失败
   - `AccessEnabler.ACCESS_ENABLER_STATUS_LOGOUT`  — 注销
- *代码*：呈现状态的原因。 如果 *状态* 是 `AccessEnabler.ACCESS_ENABLER_STATUS_SUCCESS`，则 *代码* 是一个空字符串(即，由 `AccessEnabler.USER_AUTHENTICATED` 常量)。 如果未经过身份验证，此参数可以采用以下值之一：
   - `AccessEnabler.USER_NOT_AUTHENTICATED_ERROR`  — 用户未经过身份验证。 回应 *checkAuthentication()* 当本地令牌缓存中没有有效的身份验证令牌时，方法调用。
   - `AccessEnabler.PROVIDER_NOT_SELECTED_ERROR` - AccessEnabler在上层应用程序通过后重置了身份验证状态计算机 *null* 到 `setSelectedProvider()` 中止身份验证流程。  用户可能已取消身份验证流程（例如，已按下“后退”按钮）。
   - `AccessEnabler.GENERIC_AUTHENTICATION_ERROR`  — 由于网络不可用或用户明确取消身份验证流等原因，身份验证流失败。
   - `AccessEnabler.LOGOUT`  — 由于注销操作，用户未被身份验证。

**触发者：** `checkAuthentication(), getAuthentication(), checkAuthorization()`

</br>

### checkPreauthorizedResources {#checkPreauth}

**描述：** 应用程序使用此方法来确定用户是否已获得查看特定受保护资源的授权。 此方法的主要目的是检索用于装饰UI的信息（例如，使用锁定和解锁图标指示访问状态）。

| **API调用：设置当前选定的提供程序** |
| --- |
| ```public void checkPreauthorizedResources(ArrayList<String> resources)``` |

**可用性：** v1.0+

**&lt;parameters: span=&quot;&quot; id=&quot;1&quot; translate=&quot;no&quot; /> 此 `resources` parameter是应检查其授权的资源数组。**&#x200B;列表中的每个元素都应该是一个表示资源ID的字符串。 资源ID与中的资源ID须遵守相同的限制 `getAuthorization()` 调用，即它应为程序员与MVPD或媒体RSS片段之间建立的商定值。

**已触发回调：** `preauthorizedResources()`

</br>

### preauthorizedResources {#preauthResources}

**描述：** checkPreauthorizedResources()触发的回调。 提供用户已被授权查看的资源列表。

| **API调用：设置当前选定的提供程序** |
| --- |
| ```public void checkPreauthorizedResources(ArrayList<String> resources)``` |

**可用性：**v 1.0+

**参数：** 此 `resources` parameter是用户已被授权查看的资源数组。

**触发者：** `checkPreauthorizedResources()`

<br>

### checkAuthorization {#checkAuthZ}

**描述：** 应用程序使用此方法来检查授权状态。 首先检查身份验证状态。 如果未经过身份验证， *setTokenRequestFailed()* 会触发回调，并且方法退出。 如果用户通过了身份验证，它还会触发授权流。 欲知详情，请参阅 *getAuthorization()* 方法。

| **API调用：检查授权状态** |
| --- |
| ```public void checkAuthorization(String resourceId)``` |

**可用性：** v1.0+

| **API调用：检查授权状态** |
| --- |
| ```public void checkAuthorization(String resourceId, Map<String, Object> genericData)``` |

**可用性：** v1.0+

**参数：**

- *resourceId*：用户请求授权的资源的ID。
- *数据*：包含要发送到Pay-TV pass服务的键值对的映射。 Adobe可以使用此数据启用未来的功能，而无需更改SDK。

**触发的回调：** `tokenRequestFailed(), setToken(), sendTrackingData(), setAuthenticationStatus()`

</br>

### getAuthorization {#getAuthZ}

**描述：** 应用程序使用此方法来启动授权流。 如果用户尚未经过身份验证，它还会启动身份验证流程。 如果用户通过了身份验证，Access Enabler将继续发出对授权令牌（如果本地令牌缓存中不存在有效的授权令牌）和短期媒体令牌的请求。 获得短媒体令牌后，授权流程即被视为完成。 此 *setToken()* 会触发回调，并将短媒体令牌作为参数提供给应用程序。 如果由于任何原因，授权失败， *tokenRequestFailed()* 会触发回调，并提供错误代码和详细信息。

| **API调用：启动授权流** |
| --- |
| ```public void getAuthorization(String resourceId)``` |

**可用性：** v1.0+

| **API调用：启动授权流** |
| --- |
| ```public void getAuthorization(String resourceId, Map<String, Object> genericData)``` |

**可用性：** v1.0+

**参数：**

- *resourceId*：用户请求授权的资源的ID。
- *数据*：包含要发送到Pay-TV pass服务的键值对的映射。 Adobe可以使用此数据启用未来的功能，而无需更改SDK。

**触发的回调：** `tokenRequestFailed(), setToken(), sendTrackingData()`

|     |     |
| --- | --- |
| ![](http://learn.adobe.com/wiki/images/icons/emoticons/warning.gif) | **触发了其他回调**  <br>此方法还可以触发以下回调（如果还启动了身份验证流程）： _setAuthenticationStatus()_， _displayProviderDialog()_ |

**注意：请尽量使用checkAuthorization()而不是getAuthorization()。 getAuthorization()方法将启动一个完整的身份验证流程（如果用户未经过身份验证），这可能会导致程序员端的复杂实施。**

</br>

### setToken {#setToken}

**描述：** 由Access Enabler触发的回调，通知应用程序授权流已成功完成。 短期媒体令牌还会作为参数提供。

| **回调：授权流已成功完成** |
| --- |
| ```public void setToken(String token, String resourceId)``` |

**可用性：**v 1.0+

**参数：**

- *令牌*：短期媒体令牌
- *resourceId*：获得授权的资源

**触发者：** `checkAuthorization(), getAuthorization()`

<br>

### tokenRequestFailed {#tokenRequestFailed}

**描述：** 由Access Enabler触发的回调，通知上层应用程序授权流失败。

| **回调：授权流失败** |
| --- |
| ```public void tokenRequestFailed(String resourceId, <br>        String errorCode, String errorDescription)``` |

**可用性：** v1.0+

**参数：**

- *resourceId*：获得授权的资源
- *错误代码*：与失败方案关联的错误代码。 可能的值：
   - `AccessEnabler.USER_NOT_AUTHORIZED_ERROR`  — 用户无法授权给定资源
- *errorDescription*：有关失败场景的其他详细信息。 如果此描述性字符串由于任何原因不可用，Adobe Primetime身份验证将发送空字符串>**(“”)**.  MVPD可使用此字符串传递自定义错误消息或与销售相关的消息。 例如，如果订阅者被拒绝对资源的授权，则MVPD会发送消息，例如：“您当前在包中无法访问此渠道。 如果要升级包，请单击此处。” 消息由Adobe Primetime身份验证通过此回调传递给程序员，程序员可以选择显示或忽略消息。 Adobe Primetime身份验证还可以使用此参数来提供可能导致错误的状况通知。 例如，“与提供商的授权服务通信时出现网络错误。”

**触发者：** `checkAuthorization(), getAuthorization()`

</br>

### 注销 {#logout}

**描述：** 使用此方法可启动注销流程。 注销是一系列HTTP重定向操作的结果，这是因为用户既需要从Adobe Primetime身份验证服务器注销，也需要从MVPD服务器注销。

| **API调用：启动注销流程** |
| --- |
| ```public void logout()``` |

**可用性：** v1.0+

**参数：** 无

**触发的回调：** 无

</br>

### getselectedprovider {#getSelectedProvider}

**描述：** 使用此方法可确定当前选择的提供程序。

| **API调用：确定当前选定的MVPD** |
| --- |
| ```public void getSelectedProvider()``` |

**可用性：** v1.0+

**参数：** 无

**触发的回调：** `selectedProvider()`

</br>

### selectedprovider {#selectedProvider}

**描述：** 由Access Enabler触发的回调，它将有关当前所选MVPD的信息提供给应用程序。

| **回调：有关当前所选MVPD的信息** |
| --- |
| ```public void selectedProvider(Mvpd mvpd)``` |

**可用性：** v1.0+

**参数：**

- *mvpd*：包含有关当前所选MVPD信息的对象

**触发者：** `getSelectedProvider()`

</br>

### getMetadata {#getMetadata}

**描述：** 使用此方法可检索Access Enabler库公开为元数据的信息。 应用程序可以通过提供复合MetadataKey对象来访问此信息。

| **API调用：查询AccessEnabler以获取元数据** |
| --- |
| ```public void getMetadata(MetadataKey metadataKey)``` |

**可用性：** v1.0+

有两种类型的元数据可供程序员使用：

- 静态元数据（身份验证令牌TTL、授权令牌TTL和设备ID）
- 用户元数据（用户特定的信息，例如用户ID和邮政编码；在身份验证和/或授权流期间，从MVPD传递到用户设备）

**参数：**

- *metadatakey*：封装键和args变量的数据结构，其含义如下：
   - 如果键为 `METADATA_KEY_TTL_AUTHN` 然后进行查询以获取身份验证令牌过期时间。
   - 如果键为 `METADATA_KEY_TTL_AUTHZ` 和参数包含名为=的SerializableNameValuePair对象 `METADATA_ARG_RESOURCE_ID` 和值= `[resource_id]`，然后进行查询以获取与指定资源关联的授权令牌的过期时间。
   - 如果键为 `METADATA_KEY_DEVICE_ID` 然后进行查询以获取当前设备id。 请注意，此功能默认处于禁用状态，程序员应联系Adobe以获取有关启用和费用的信息。
   - 如果键为 `METADATA_KEY_USER_META` 和参数包含名为=的SerializableNameValuePair对象 `METADATA_KEY_USER_META` 和值= `[metadata_name]`，则查询用户元数据。 可用用户元数据类型的当前列表：
      - `zip`  — 邮政编码
      - `householdID`  — 家庭标识符。 如果MVPD不支持子帐户，则它与 `userID`.
      - `maxRating`  — 用户的最大家长评级
      - `userID`  — 用户标识符。 如果MVPD支持子帐户，并且用户不是主帐户，
      - `channelID`  — 用户有权查看的渠道列表

程序员可用的实际用户元数据取决于MVPD提供的内容。  此列表将随着新元数据的推出和添加到Adobe Primetime身份验证系统中而进一步扩展。

**触发的回调：** [`setMetadataStatus()`](#setMetadaStatus)

**更多信息：** [用户元数据](#setmetadatastatus)

</br>

### setmetadatastatus {#setMetadaStatus}

**描述：** 由Access Enabler触发的回调，用于提供通过 *getMetadata()* 呼叫。

| **回调：元数据检索请求的结果** |
| --- |
| ```public void setMetadataStatus(MetadataKey key, MetadataStatus result)``` |

**可用性：** v1.0+

**参数：**

- *键*：MetadataKey对象，其中包含为其请求元数据值的键和相关参数（请参阅演示应用程序以了解参考实施）。
- *结果*：包含所请求元数据的复合对象。 该对象具有以下字段：
   - *simpleResult*：一个字符串，表示在请求身份验证TTL、授权TTL或设备ID时的元数据值。 如果为用户元数据发出请求，则此值为null。

   - *userMetadataResult*：包含JSON用户元数据有效负载的Java表示法的对象。 例如：

     ```json
     {
     "street": "Main Avenue",
     "buildings": ["150", "320"]
     }
     ```

     翻译为Java的形式：

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


请求简单元数据（身份验证TTL、授权TTL或设备ID）时，该值为空。

- *已加密*：指定是否对检索到的元数据进行加密的布尔值。 此参数仅对用户元数据请求有意义，对于始终未加密接收的静态元数据（例如，身份验证TTL）没有意义。 如果此参数设置为True，则程序员需要通过使用白名单私钥（与在中签名请求者ID时使用的私钥）执行RSA解密来获取未加密的用户元数据值。 [`setRequestor`](#setRequestor) 调用)。

**触发者：** [`getMetadata()`](#getMetadata)

**更多信息：** [用户元数据](/help/authentication/user-metadata.md)

</br>

## getVersion {#getVersion}

**描述：** 使用此方法检索AccessEnabler当前版本

| **API调用：获取AccessEnabler版本** |
| --- |
| ```public static String getVersion()``` |

## 跟踪事件 {#tracking}

Access Enabler会触发一个附加回调，该回调不一定与权利文件流相关。 实现名为的事件跟踪回调函数 *sendTrackingData()* 是可选的，但它使应用程序能够跟踪特定事件并编译统计信息，如成功/失败的身份验证/授权尝试次数。 以下是 *sendTrackingData()* 回调：

### sendTrackingData {#sendTrackingData}

**描述：** Access Enabler向应用程序发出各种事件（如身份验证/授权流的完成/失败）的信号时触发的回调。 sendTrackingData()还会报告设备类型、Access Enabler客户端类型和操作系统。

>[!WARNING]
>
> 设备类型和操作系统通过使用公共Java库(http://java.net/projects/user-agent-utils)和用户代理字符串派生。 请注意，此信息仅以粗略的方式提供，用于按设备类别细分操作量度，但该Adobe对错误结果不承担任何责任。 请相应地使用新功能。

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
   - `tvos`
   - `android`
   - `firetv`

| 回调：跟踪事件 |
| --- |
| ```public void sendTrackingData(Event event, ArrayList<String> data)``` |

**可用性：** v1.0+

**参数：**

- *事件*：正在跟踪的事件。 有三种可能的跟踪事件类型：
   - **授权检测：** 每当授权令牌请求返回时(事件类型为 `EVENT_AUTHZ_DETECTION`)
   - **authenticationDetection：** 每当进行身份验证检查时(事件类型为 `EVENT_AUTHN_DETECTION`)
   - **mvpdSelection：** 当用户在MVPD选择表单中选择MVPD时(事件类型为 `EVENT_MVPD_SELECTION`)
- *数据*：与所报告事件关联的其他数据。 此数据以值列表的形式提供。

以下说明用于解释 *数据* 数组：

- 对于事件类型 *`EVENT_AUTHN_DETECTION`：*
   - **0**  — 令牌请求是否成功(true/false)，如果以上为true：
   - **1** - MVPD ID字符串
   - **2** - GUID（md5散列）
   - **3**  — 令牌已在缓存中(true/false)
   - **4**  — 设备类型
   - **5** - Access Enabler客户端类型
   - **6**  — 操作系统类型

- 对于事件类型 `EVENT_AUTHZ_DETECTION`
   - **0**  — 令牌请求是否成功(true/false)，如果成功：
   - **1** - MVPD ID
   - **2** - GUID（md5散列）
   - **3**  — 令牌已在缓存中(true/false)
   - **4**  — 错误
   - **5**  — 详细信息
   - **6**  — 设备类型
   - **7** - Access Enabler客户端类型
   - **8**  — 操作系统类型

- 对于事件类型 `EVENT_MVPD_SELECTION`
   - **0**  — 当前所选MVPD的ID
   - **1**  — 设备类型
   - **2** - Access Enabler客户端类型
   - **3**  — 操作系统类型

**触发者：** `checkAuthentication(), getAuthentication(), checkAuthorization(), getAuthorization(), setSelectedProvider()`
