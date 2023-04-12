---
title: Amazon FireOS SDK，带有动态客户端注册
description: Amazon FireOS SDK，带有动态客户端注册
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 0%

---


# Amazon FireOS SDK，带有动态客户端注册 {#amazon-fireos-sdk-with-dynamic-client-registration}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

</br>

## <span id=""></span>简介 {#Intro}

FireOS AccessEnabler SDK for FireTV已修改为在不使用会话Cookie的情况下启用身份验证。 随着越来越多的浏览器限制对Cookie的访问，需要使用另一种方法来允许身份验证。

**FireOS SDK 3.0.4** 将基于签名请求者ID和会话cookie身份验证的当前应用程序注册机制替换为 [动态客户端注册](/help/authentication/dynamic-client-registration.md).
 

## API更改 {#API}

### Factory.getInstance

**描述：** 实例化Access Enabler对象。 每个应用程序实例应有一个Access Enabler实例。

| API调用：构造函数 |
| --- |
| public static AccessEnabler getInstance(ContextAppContext， String softwareStatement， String redirectUrl)<br>        引发AccessEnablerException |

**可用性：** v3.0+

**参数：**

- *appContext*:Android应用程序上下文
- *softwareStatement*:从TVE仪表板或 *null* 如果在strings.xml中设置了“software\_statement”
- *redirectUrl* :对于FireTV实施，此参数应为null。 此属性的任何设置都将被忽略。 

**注释**

- 无效的softwareStatement将导致应用程序无法初始化AccessEnabler或注册应用程序以进行Adobe Pass身份验证和授权
- FireTV的redirectUrl参数由SDK设置为adobepass://android.app as身份验证，由唯一的AccessEnabler实例处理。

### setRequestor

**描述：** 确定渠道的标识。 在向Adobe Primetime身份验证系统的Adobe注册时，会为每个渠道分配一个唯一ID。 在处理SSO和远程令牌时，当应用程序处于后台时，身份验证状态可能会发生更改，当应用程序进入前台时，可以再次调用setRequestor以与系统状态同步（如果启用了SSO，则获取远程令牌，如果同时发生注销，则删除本地令牌）。

服务器响应包含MVPD列表以及附加到渠道标识的一些配置信息。 服务器响应由Access Enabler代码在内部使用。 只有操作的状态（即SUCCESS/FAIL）会通过setRequestorComplete()回调函数显示给您的应用程序。

如果 *url* 参数，则生成的网络调用将定向默认的服务提供商URL:Adobe发布生产环境。

如果为 *url* 参数，则生成的网络调用将定向 *url* 参数。 所有配置请求都在单独的线程中同时触发。 编译MVPD列表时，优先使用第一个响应者。 对于列表中的每个MVPD，访问启用码会记住相关服务提供商的URL。 所有后续授权请求都会被定向到与配置阶段中与目标MVPD配对的服务提供商关联的URL。

| API调用：请求者配置 |
| --- |
| public void setRequestor(String requestorId) |

**可用性：** v3.0+

| API调用：请求者配置 |
| --- |
| ```public void setRequestor(String requestorId, ArrayList<String> urls)``` |

**可用性：** v3.0+

**参数：**

- *requestorID*:与渠道关联的唯一ID。 在您首次向Adobe Primetime身份验证服务注册时，将由Adobe分配的唯一ID传递到您的网站。
- *url*:可选参数；默认情况下，使用Adobe服务提供商(http://sp.auth.adobe.com/)。 此数组允许您为由Adobe提供的身份验证和授权服务指定端点（可能出于调试目的而使用不同的实例）。 您可以使用它指定多个Adobe Primetime身份验证服务提供程序实例。 这样做时，MVPD列表由所有服务提供商的端点组成。 每个MVPD都与最快的服务提供商关联；即首先响应并支持该MVPD的提供商。

已弃用：

- *signedRequestorID*:使用您的私钥进行数字签名的请求者ID的副本。 <!--For more details, see [Registering Native Clients](http://tve.helpdocsonline.com/registering-native-clients)-->.

**触发的回调：** `setRequestorComplete()`

</br>

### 注销

**描述：** 使用此方法启动注销流程。 注销是一系列HTTP重定向操作的结果，因为用户需要从Adobe Primetime身份验证服务器以及MVPD服务器中注销。 因此，此流程将打开一个ChromeCustomTab窗口以执行注销。

| API调用：启动注销流程 |
| --- |
| 公共撤销注销() |

**可用性：** v3.0+

**参数：** 无

**触发的回调：** `setAuthenticationStatus()`

## 程序员实施流程 {#Progr}

### **1. 注册申请** 

1. 从Adobe Pass获取software\_statement(TVE Dashboard)
1. 有两个选项可将这些值传递到Adobe Pass SDK:
   - 在strings.xml中，添加： 

      ```
      <string name>"software\_statement">[softwarestatement value]</string>
      ```

   - 调用AccessEnabler.getInstance(appContext，softwareStatement， null)

 

### **2. 配置应用程序**

- a. setRequestor(requestor\_id) 

   SDK将执行以下操作： 

   - 注册申请：使用 **software\_statement**,SDK将获取 **client\_id， client\_secret， client\_id\_issued\_at, redirect\_uris， grant\_types**. 此信息将存储在应用程序的内部存储中。
   - 获取 **access\_token** 使用client\_id、client\_secret和grant\_type=&quot;client\_credentials&quot;。 此access\_token将用于SDK对Adobe Pass服务器进行的每次调用。

| 令牌错误响应： |  |  |
|--- | --- | --- |
| HTTP 400（请求错误） | {&quot;error&quot;:&quot;invalid\_request&quot;} | 该请求缺少必需的参数，包括不受支持的参数值（除授予类型外），重复参数，包括多个凭据，使用多个机制对客户端进行身份验证，或者格式不正确。 |
| HTTP 400（请求错误） | {&quot;error&quot;:&quot;无效\_client&quot;} | 客户端身份验证失败，因为客户端未知。 SDK *必须* 再次向授权服务器注册。 |
| HTTP 400（请求错误） | {&quot;error&quot;:&quot;unauthed\_client&quot;} | 已验证的客户端无权使用此授权授权类型。 |

- 如果MVPD需要被动身份验证，则WebView将打开以使用该MVPD执行被动身份验证，并在完成后关闭

- b. checkAuthentication()

   - *true* :转到授权
   - *false* :转到选择MVPD

- c.getAuthentication :SDK将包含 **access_token** 在调用参数中 

   - mvpd记住：转到setSelectedProvider(mvpd\_id)
   - 未选择mvpd :displayProviderDialog
   - 已选择mvpd:转到setSelectedProvider(mvpd\_id)

- d.setSelectedProvider

   - mvpd\_id身份验证url已加载到ChromeCustomTabs中
   - 登录成功：delegate.setAuthenticationStatus(SUCCESS)
   - 已取消登录：重置MVPD选择
   - URL方案建立为“adobepass://android.app”，用于在身份验证完成时捕获

- e.get/checkAuthorization :SDK将在标头中包**access\_token**作为授权：持有者 **access\_token**

- 如果授权成功，将进行调用以获取媒体令牌

- f.注销： 

   - SDK将删除当前请求者的有效令牌（由其他应用程序获取且未通过SSO进行的身份验证将保持有效）
   - SDK将打开Chrome自定义选项卡以访问mvpd\_id注销端点。 完成后，将关闭Chrome自定义选项卡
   - URL方案建立为“adobepass://logout”以捕获注销完成时的时刻
   - logout将触发sendTrackingData(new Event(EVENT\_LOGOUT，USER\_NOT\_AUTHENTICATED\_ERROR)和回调：setAuthenticationStatus(0,&quot;Logout&quot;)

 

**注意：** 因为每个调用都需要 **access_token**,SDK中会处理以下可能的错误代码。 

| 错误响应 |  |  |
|--- | --- | --- |
| invalid_request | 400 | 请求的格式错误。 SDK应停止执行对服务器的调用。 |
| invalid_client | 403 | 不再允许客户端ID执行请求。 sdk必须再次执行客户端注册。 |
| access_denied | 401 | access_token无效。 sdk必须请求新的access_token。 |

