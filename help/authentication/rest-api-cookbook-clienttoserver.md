---
title: REST API指南（客户端到服务器）
description: 服务器的REST API指南客户端。
source-git-commit: 4c3a0dd56b4ef99ac8c57cfde61f792088b0ff4d
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 0%

---


# REST API指南（客户端到服务器） {#rest-api-cookbook-client-to-server}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。


## 概述 {#overview}

本文档分步说明程序员工程团队如何集成“智能设备”（游戏控制台、智能电视应用程序、机顶盒等） 使用REST API服务进行Adobe Primetime身份验证。 这种客户端到服务器方法使用REST API而不是客户端SDK，它允许对不同平台提供更广泛的支持，对于这些平台，开发大量唯一SDK是不可行的。 有关无客户端解决方案工作原理的广泛技术概述，请参阅 [无客户端技术概述](/help/authentication/rest-api-overview.md).


此方法需要两个组件（流应用程序和AuthN应用程序）才能完成所需的流程：流应用程序中的启动、注册、授权和视图媒体流，以及AuthN应用程序中的身份验证流程。

## 组件 {#components}

在工作的客户端到服务器解决方案中，涉及以下组件：

 

| 类型 | 组件 | 描述 |
| --- | --- | --- |
| 流设备 | 流应用程序 | 驻留在用户流设备上并播放经过验证的视频的程序员应用程序。 |
|  | \[可选\] AuthN模块 | 如果流设备具有用户代理（即Web浏览器），则AuthN模块负责在MVPD IdP上对用户进行身份验证。 |
| \[可选\] AuthN设备 | AuthN应用程序 | 如果流设备没有用户代理（即Web浏览器），则AuthN应用程序是使用Web浏览器从单独用户设备访问的程序员Web应用程序。  |
| Adobe基础架构 | Adobe Pass服务 | 与MVPD IdP和AuthZ服务集成并提供身份验证和授权决策的服务。 |
| MVPD基础架构 | MVPD IdP | 提供基于凭据的身份验证服务以验证其用户身份的MVPD端点。 |
|  | MVPD AuthZ服务 | MVPD端点，根据用户的订阅、家长控制等提供授权决策。 |

 

流程中使用的其他术语在 [术语表](http://tve.helpdocsonline.com/adobe-pass-glossary).

## 流量{#flows}

### 动态客户端注册(DCR)

Adobe Pass使用DCR保护程序员应用程序或服务器与Adobe Pass服务之间的客户端通信。 DCR流是独立的、从属的和先决条件的流，可在此处找到：http://tve.helpdocsonline.com/dynamic-client-registration


### 流（智能设备）应用程序流

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/clientless_1st_screen_updated.PNG)

 

#### 启动流程

1. 您的应用程序启动并加载其初始UI。

2. 获取/生成设备ID。

3. 发出检查身份验证调用，以查看设备是否已经过身份验证。  例如： [`<SP_FQDN>/api/v1/checkauthn [device ID]`](/help/authentication/check-authentication-token.md)

4. 如果 `checkauthn` 调用成功，从步骤2开始继续执行授权流程。  如果注册流失败，请启动注册流程。

 

#### 注册流程

1. 获取注册代码和URL，供用户用于访问第2个屏幕登录应用程序，并将这些代码和URL呈现给用户：

   a.向Adobe注册代码服务发送POST请求，以传递经过哈希处理的设备ID和“注册URL”。  例如： [`<REGGIE_FQDN>/reggie/v1/[requestorId]/regcode [device ID]`](/help/authentication/registration-code-request.md)

   b.向用户显示返回的注册代码和URL。

   c.指示用户切换到能够使用Web的设备，导航到URL，然后输入注册代码。

 

#### 授权流程

1. 用户从第2个屏幕应用程序返回，然后按下设备上的“继续”按钮。 或者，您也可以实施轮询机制来检查身份验证状态，但Adobe Primetime身份验证建议使用“继续”按钮方法来替代轮询。 <!--(For information on employing a "Continue" button versus polling the Adobe Primetime authentication backend server, see the Clientless Technical Overview: Managing 2nd-Screen Workflow Transition.)--> 例如： [\&lt;sp _fqdn=&quot;&quot;>/api/v1/tokens/authn](/help/authentication/retrieve-authentication-token.md)

2. 向Adobe Primetime身份验证授权服务发送GET请求以启动授权。 例如： `<SP_FQDN>/api/v1/authorize [device ID, Requestor ID, Resource ID]`

<!-- end list -->

- 如果响应指示成功：用户具有有效的AuthN令牌，且用户有权观看请求的媒体（此用户具有有效的AuthZ令牌）。

- 如果响应指示失败：检查引发的异常以确定其类型（AuthN、AuthZ或其他内容）：

   - 如果是AuthN错误，则重新启动注册流程。

   - 如果是AuthZ错误，则用户无权观看请求的媒体，应向用户显示某种错误消息。

   - 如果存在其他错误（连接错误、网络错误等） 然后向用户显示相应的错误消息。

 

#### 查看媒体流量

1. 提供媒体选项。 用户选择要查看的媒体。

2. 介质是否受保护？

   a.您的应用程序会检查媒体是否受保护。

   b.如果媒体受到保护，则您的应用程序将启动上述授权(AuthZ)流程。

   c.如果媒体未受到保护，则为用户播放媒体。

3. 播放媒体。


### AuthN（第2屏幕）应用程序流

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/smart_dev_second_flow.png)

1. 获取此用户的MVPD列表。 例如： [`<SP_FQDN>/api/v1/config/[requestorID]`](/help/authentication/provide-mvpd-list.md)

1. 启动身份验证流程。  例如： [`<SP_FQDN>/api/v1/authenticate [requestorID, MVPD ID, Redirect URL, Domain name, Registration Code, "noflash=true"]`](/help/authentication/initiate-authentication.md)

1. 检查身份验证是否成功。  例如： [`<SP_FQDN>/api/v1/checkauthn/[registration code][requestor ID]`](/help/authentication/check-authentication-token.md)

1. 将用户发送回您的智能设备应用程序以完成授权流程。

 

## 平台SSO {#platform-sso}

某些平台为单点登录(SSO)提供专用支持。 可以找到每个相应平台的实施详细信息：

- [Apple SSO](http://tve.helpdocsonline.com/rest-api-apple-sso)
- Amazon SSO

## 适用于REST API的TempPass和促销TempPass {#temppass}

对于不需要用户输入凭据的TempPass和促销TempPass实施，可以直接在流应用程序中实施身份验证。 

**要使用此API，流应用程序需要确保设备ID的唯一性，因为它用于标识令牌以及可选的额外数据。**


![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/Free%20preview%20option.png?dc=201612071020-0)

### 相关信息 {#related}

- [REST API引用](/help/authentication/rest-api-reference.md)
