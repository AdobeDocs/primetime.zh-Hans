---
title: 带有动态客户端注册功能的Amazon FireOS SDK
description: 带有动态客户端注册功能的Amazon FireOS SDK
exl-id: 27acf3f5-8b7e-4299-b0f0-33dd6782aeda
source-git-commit: bfa2c3d55848dd1e50daa83fb77d040bc7c37045
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 0%

---

# 带有动态客户端注册功能的Amazon FireOS SDK {#amazon-fireos-sdk-with-dynamic-client-registration}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权使用。

</br>

## <span id=""></span>介绍 {#Intro}

已修改适用于FireTV的FireOS AccessEnabler SDK，以便在不使用会话Cookie的情况下启用身份验证。 随着越来越多的浏览器限制对Cookie的访问，需要另一种方法来允许身份验证。

**FireOS SDK 3.0.4** 将基于已签名请求者ID和会话Cookie身份验证的当前应用程序注册机制替换为 [动态客户端注册](/help/authentication/dynamic-client-registration.md).


## API更改 {#API}

### Factory.getInstance

**描述：** 实例化访问启用程序对象。 每个应用程序实例应有一个访问启用程序实例。

| API调用：构造函数 |
| --- |
| 公共静态AccessEnabler getInstance(Context appContext， String softwareStatement， String redirectUrl)<br>        引发AccessEnablerException |

**可用性：** v3.0+

**参数：**

- *appContext*：Android应用程序上下文
- *softwarestatement*：从TVE功能板或获得的值 *null* 如果在strings.xml中设置了“software\_statement”
- *redirectUrl* ：对于FireTV实施，此参数应为空。 此属性上的任何设置都将被忽略。

**注释**

- softwareStatement无效将导致应用程序无法初始化AccessEnabler或注册Adobe Pass身份验证和授权的应用程序
- FireTV的redirectUrl参数由SDK设置为adobepass://android.app ，因为身份验证由唯一的AccessEnabler实例处理。

### setRequestor

**描述：** 建立渠道的标识。 在为Adobe Primetime身份验证系统注册Adobe时，每个渠道都会分配一个唯一的ID。 在处理SSO和远程令牌时，当应用程序处于后台时，身份验证状态可能会更改，当应用程序进入前台时，可以再次调用setRequestor以便与系统状态同步（如果启用了SSO，则获取远程令牌，如果同时发生注销，则删除本地令牌）。

服务器响应包含MVPD列表以及附加到通道标识的一些配置信息。 服务器响应由访问启用码在内部使用。 通过setRequestorComplete()回调只向应用程序显示操作的状态（即SUCCESS/FAIL）。

如果 *url* 未使用参数，生成的网络调用将定向默认服务提供商URL：Adobe发布生产环境。

如果为提供了值， *url* 参数，则生成的网络调用将定向于 *url* 参数。 所有配置请求都在单独的线程中同时触发。 在编译MVPD列表时，优先使用第一个响应程序。 对于列表中的每个MVPD， Access Enabler记住关联服务提供商的URL。 所有后续权利请求都定向到与服务提供程序相关联的URL，该URL在配置阶段与目标MVPD配对。

| API调用：请求者配置 |
| --- |
| 公共void setRequestor(String requestorId) |

**可用性：** v3.0+

| API调用：请求者配置 |
| --- |
| ```public void setRequestor(String requestorId, ArrayList<String> urls)``` |

**可用性：** v3.0+

**参数：**

- *请求者ID*：与渠道关联的唯一ID。 首次注册Adobe Primetime身份验证服务时，请将Adobe分配的唯一ID传递到您的网站。
- *url*：可选参数；默认情况下，使用Adobe服务提供程序(http://sp.auth.adobe.com/)。 此阵列允许您为Adobe提供的身份验证和授权服务指定端点（其他实例可能用于调试目的）。 您可以使用此项指定多个Adobe Primetime身份验证服务提供程序实例。 这样做时，MVPD列表由来自所有服务提供商的端点组成。 每个MVPD都与最快的服务提供程序相关联；即首先响应并支持该MVPD的服务提供程序。

已弃用：

- *signedRequestID*：使用您的私钥进行数字签名的请求者ID的副本。 <!--For more details, see [Registering Native Clients](http://tve.helpdocsonline.com/registering-native-clients)-->.

**触发的回调：** `setRequestorComplete()`

</br>

### 注销

**描述：** 使用此方法可启动注销流程。 注销是一系列HTTP重定向操作的结果，这是因为用户既需要从Adobe Primetime身份验证服务器注销，也需要从MVPD服务器注销。 因此，此流程将打开一个ChromeCustomTab窗口以执行注销。

| API调用：启动注销流程 |
| --- |
| public void logout() |

**可用性：** v3.0+

**参数：** 无

**触发的回调：** `setAuthenticationStatus()`

## 程序员实施流程 {#Progr}

### **1. 注册应用程序**

1. 从Adobe Pass获取software\_statement （ TVE功能板）
1. 可使用以下两个选项将这些值传递到Adobe Pass SDK：
   - 在strings.xml中，添加：

     ```
     <string name>"software\_statement">[softwarestatement value]</string>
     ```

   - 调用AccessEnabler.getInstance(appContext，softwareStatement， null)



### **2. 配置应用程序**

- a. setRequestor(requestor\_id)

  SDK将执行以下操作：

   - 注册应用程序：使用 **software\_statement**，SDK将获取 **client\_id， client\_secret， client\_id\_issued\_at， redirect\_uris， grant\_types**. 此信息将存储在应用程序的内部存储中。
   - 获取 **access\_token** 使用client\_id、client\_secret和grant\_type=&quot;client\_credentials&quot; 。 此access\_token将用于SDK对Adobe Pass服务器进行的每次调用。

| 令牌错误响应： |  |  |
|--- | --- | --- |
| HTTP 400（错误请求） | {&quot;error&quot;： &quot;invalid\_request&quot;} | 请求缺少必需的参数，包括不受支持的参数值（授予类型除外），重复参数，包括多个凭据，利用多个机制来验证客户端，或者格式不正确。 |
| HTTP 400（错误请求） | {&quot;error&quot;： &quot;invalid\_client&quot;} | 客户端身份验证失败，因为客户端未知。 SDK *必须* 请再次向授权服务器注册。 |
| HTTP 400（错误请求） | {&quot;error&quot;： &quot;unauthorized\_client&quot;} | 经过身份验证的客户端无权使用此授权授予类型。 |

- 如果MVPD需要被动身份验证，则WebView将打开以使用该MVPD执行被动身份验证，并在完成后关闭

- b. checkAuthentication()

   - *true* ：转到授权
   - *false* ：转到选择MVPD

- c. getAuthentication ：SDK将包含 **access_token** 在调用参数中

   - 记住mvpd ：转到setSelectedProvider(mvpd\_id)
   - 未选择mvpd ：displayProviderDialog
   - 已选择mvpd ：转到setSelectedProvider(mvpd\_id)

- d. setSelectProvider

   - mvpd\_id身份验证URL加载到ChromeCustomTables中
   - 登录成功：delegate.setAuthenticationStatus ( SUCCESS )
   - 已取消登录：重置MVPD选择
   - URL方案将建立为“adobepass://android.app”，以便在身份验证完成时捕获

- e. get/checkAuthorization ： SDK将在标头中包含**access\_token **作为授权：持有者 **access\_token**

- 如果授权成功，将调用以获取媒体令牌

- f.注销：

   - SDK将删除当前请求者的有效令牌（由其他应用程序而非通过SSO获得的身份验证将保持有效）
   - SDK将打开Chrome自定义选项卡以访问mvpd\_id注销端点。 完成后，Chrome自定义选项卡将关闭
   - URL方案将建立为“adobepass://logout”，以捕获注销完成时的时间
   - 注销将触发sendTrackingData(new Event(EVENT\_LOGOUT，USER\_NOT\_AUTHENTICATED\_ERROR)和回调：setAuthenticationStatus(0，&quot;Logout&quot;)



**注意：** 因为每个调用需要 **access_token**，则在SDK中处理以下可能的错误代码。

| 错误响应 |  |  |
|--- | --- | --- |
| invalid_request | 400 | 请求的格式不正确。 SDK应停止执行对服务器的调用。 |
| invalid_client | 403 | 不再允许客户端id执行请求。 sdk必须再次执行客户端注册。 |
| access_denied | 401 | access_token无效。 sdk必须请求新的access_token。 |
