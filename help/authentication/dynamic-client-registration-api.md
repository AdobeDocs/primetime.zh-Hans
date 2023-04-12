---
title: 动态客户端注册API
description: 动态客户端注册API
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---


# 动态客户端注册API {#dynamic-client-registration-api}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## 概述 {#overview}

目前，Primetime身份验证可通过两种方式来识别和注册应用程序：

* 基于浏览器的客户端通过允许的方式进行注册 [域列表](/help/authentication/programmer-overview.md)
* 本机应用程序客户端(如iOS和Android应用程序)通过签名请求器机制进行注册。

Adobe Primetime身份验证为注册应用程序提出了一种新机制。 以下各段介绍了这一机制。

## 申请登记机制 {#appRegistrationMechanism}

### 技术原因 {#reasons}

Adobe Primetime身份验证中的身份验证机制依赖于会话Cookie，但由于 [Android Chrome自定义选项卡](https://developer.chrome.com/multidevice/android/customtabs){target=_blank} and [Apple Safari View Controller](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller){target=_blank}，则无法再实现此目标。

鉴于这些限制，Adobe为其所有客户引入了新的注册机制。 它基于OAuth 2.0 RFC，包含以下步骤：

1. 从TVE Dashboard检索软件语句
1. 获取客户端凭据
1. 获取访问令牌

### 从TVE仪表板检索软件语句 {#softwareStatement}

对于您发布的每个应用程序，您需要获取一份软件声明。 在创建应用程序后，所有软件语句都通过TVE Dashboard提供。 软件语句应与用户设备上的应用程序一起部署。

>[!IMPORTANT]
>
>使用软件语句时，不再需要签名的请求者ID机制。

有关如何创建软件语句的更多详细信息，请访问 [TVE仪表板中的客户注册](/help/authentication/dynamic-client-registration.md).

### 获取客户端凭据 {#clientCredentials}

从TVE Dashboard中检索软件语句后，需要在Adobe Primetime授权服务器上注册您的应用程序。 为此，请执行/register调用并检索您的唯一客户端标识符。

**请求**

| HTTP调用 |  |
|-----------|--------------------|
| 路径 | /o/client/register |
| 方法 | POST |

| 字段 |  |  |
|--------------------|---------------------------------------------------------------------------|-----------|
| software_statement | 在TVE Dashboard中创建的软件语句。 | 强制 |
| redirect_uri | 应用程序用于完成身份验证流程的URI。 | 可选 |

| 请求头 |  |  |
|-----------------|--------------------------------------------------------------------------------|-----------|
| Content-Type | application/json | 强制 |
| X-Device-Info | 传递设备和连接信息中定义的设备信息 | 强制 |
| User-Agent | 用户代理 | 强制 |

**响应**

| 响应头 |  |  |
|------------------|------------------|-----------|
| Content-Type | application/json | 强制 |

| 响应字段 |  |  |
|---------------------|-----------------|----------------------------|
| client_id | 字符串 | 强制 |
| client_secret | 字符串 | 强制 |
| client_id_issued_at | long | 强制 |
| redirect_uris | 字符串列表 | 强制 |
| grant_types | 字符串列表<br/> **接受值**<br/> `client_credentials`:由不安全的客户端（如Android SDK）使用。 | 强制 |
| 错误 | **接受的值**<ul><li>invalid_request</li><li>invalid_redirect_uri</li><li>invalid_software_statement</li><li>unapproved_software_statement</li></ul> | 错误流中的必需项 |


#### 错误响应 {#error-response}

如果出现错误，注册服务器将使用HTTP 400（错误请求）状态代码进行响应，并在响应中包含以下参数：

| 状态代码 | 响应体 | 描述 |
| --- | --- | --- |
| HTTP 400 | {&quot;error&quot;:&quot;invalid_request&quot;} | 请求缺少必需的参数、包含不受支持的参数值、重复参数，或者其格式不正确。 |
| HTTP 400 | {&quot;error&quot;:&quot;invalid_redirect_uri&quot;} | 基于此客户端的注册应用程序，不允许此客户端使用redirect_uri。 |
| HTTP 400 | {&quot;error&quot;:&quot;invalid_software_statement&quot;} | 软件语句无效。 |
| HTTP 400 | {&quot;error&quot;:&quot;unapproved_software_statement&quot;} | 在配置中未找到software_id。 |

#### 客户端凭据示例 {#client-credentials-example}

**请求：**

```HTTPS
POST /o/client/register HTTP/1.1
    User-Agent: Android
    X-Device-Info: ew0KICAibW9kZWwiOiAiVFYiLA0KICAidmVuZG9yIjogIkFwcGxlIiwNCiAgIm1hbnVmYWN0dXJlciI6ICJBcHBsZSIsDQogICJvc05hbWUiOiAidHZPUyIsDQogICJvc1ZlbmRvciI6ICJBcHBsZSIsDQogICJvc1ZlcnNpb24iOiAiMTAuMiIsDQogICJicm93c2VyVmVuZG9yIjogIkFwcGxlIiwNCiAgImJyb3dzZXJOYW1lIjogIlNhZmFyaSINCn0
    Content-Type: application/json
    Accept: application/json
    Host: sp.auth.adobe.com
 {
        "software_statement": "eyJhbGciOiJSUzI1NiJ9.
    eyJzb2Z0d2FyZV9pZCI6IjROUkIxLTBYWkFCWkk5RTYtNVNNM1IiLCJjbGll
    bnRfbmFtZSI6IkV4YW1wbGUgU3RhdGVtZW50LWJhc2VkIENsaWVudCIsImNs
    aWVudF91cmkiOiJodHRwczovL2NsaWVudC5leGFtcGxlLm5ldC8ifQ.
    GHfL4QNIrQwL18BSRdE595T9jbzqa06R9BT8w409x9oIcKaZo_mt15riEXHa
    zdISUvDIZhtiyNrSHQ8K4TvqWxH6uJgcmoodZdPwmWRIEYbQDLqPNxREtYn0
    5X3AR7ia4FRjQ2ojZjk5fJqJdQ-JcfxyhK-P8BAWBd6I2LLA77IG32xtbhxY
    fHX7VhuU5ProJO8uvu3Ayv4XRhLZJY4yKfmyjiiKiPNe-Ia4SMy_d_QSWxsk
    U5XIQl5Sa2YRPMbDRXttm2TfnZM1xx70DoYi8g6czz-CPGRi4SW_S2RKHIJf
    IjoI3zTJ0Y2oe0_EJAiXbL6OyF9S5tKxDXV8JIndSA",
  "redirect_uri": "adobepass://com.programmer"  }
```

**响应：**

```HTTPS
HTTP/1.1 201 Created
Content-Type: application/json
Cache-Control: no-store
Pragma: no-cache
    
{
 "client_id": "s6BhdRkqt3",
 "client_secret": "t7AkePiru4",
 "client_id_issued_at": 2893256800,
 "redirect_uris": [
   "app://com.programmer.adobe#sdasdsadas"],
 "grant_types": ["client_credentials"]
}
```

**错误响应：**

```HTTPS
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8
Cache-Control: no-store
Pragma: no-cache
    
{ "error": "invalid_request" }
```

### 获取访问令牌 {#accessToken}

在检索应用程序的唯一客户端标识符（客户端ID和客户端密钥）后，您需要获取访问令牌。 访问令牌是强制性的OAuth 2.0令牌，用于调用Primetime身份验证API。

>[!NOTE]
>
>目前，访问令牌的存留时间为24小时。

**请求**


| **HTTP调用** |  |
| --- | --- |
| 路径 | `/o/client/token` |
| 方法 | POST |

| **请求参数** |  |
| --- | --- |
| `grant_type` | 在客户端注册过程中收到。<br/> **接受的值**<br/>`client_credentials`:用于不安全的客户端，例如Android SDK。 |
| `client_id` | 在客户端注册过程中获取的客户端标识符。 |
| `client_secret` | 在客户端注册过程中获取的客户端标识符。 |

**响应**

| 响应字段 |  |  |
| --- | --- | --- |
| `access_token` | 您应用于调用Primetime API的访问令牌值 | 强制 |
| `expires_in` | access_token过期之前的时间（以秒为单位） | 强制 |
| `token_type` | 令牌的类型 **载体** | 强制 |
| `created_at` | 令牌的问题时间 | 强制 |
| **响应头** |  |  |
| `Content-Type` | application/json | 强制 |

**错误响应**

如果出现错误，授权服务器将回复HTTP 400（错误请求）状态代码，并在响应中包含以下参数：

| 状态代码 | 响应体 | 描述 |
| --- | --- | --- |
| HTTP 400 | {&quot;error&quot;:&quot;invalid_request&quot;} | 该请求缺少必需的参数，包括不受支持的参数值（除授予类型外），重复参数，包括多个凭据，使用多个机制对客户端进行身份验证，或者格式不正确。 |
| HTTP 400 | {&quot;error&quot;:&quot;invalid_client&quot;} | 客户端身份验证失败，因为客户端未知。 SDK必须再次向授权服务器注册。 |
| HTTP 400 | {&quot;error&quot;:&quot;unauthorized_client&quot;} | 已验证的客户端无权使用此授权授权类型。 |

#### 获取访问令牌示例： {#obt-access-token}

**请求：**

```HTTPS
POST o/client/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
    
grant_type=client_credentials&client_id=AAA&client_secret=SSS
```

**响应：**

```JSON
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8
Cache-Control: no-store
Pragma: no-cache
    
{
  "access_token":"2YotnFZFEjr1zCsicMWpAA",
  "token_type":"bearer",
  "expires_in":3600,
  "created_at":123456789
}
```

**错误响应：**

```JSON
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8
Cache-Control: no-store
Pragma: no-cache
    
{ "error": "invalid_request" }
```

## 执行身份验证请求 {#autheticationRequests}

使用访问令牌执行Adobe Primetime [身份验证API调用](/help/authentication/initiate-authentication.md). 要实现此目的，需要通过以下方式之一将访问令牌添加到API请求中：

* 向请求中添加新查询参数。 该新参数称为 **access_token**.

* 通过向请求添加新的HTTP标头：授权：持票人。 我们建议您使用HTTP标头，因为查询字符串在服务器日志中往往可见。

如果发生错误，可返回以下错误响应：

| 错误响应 |  |  |
|-----------------|-----|--------------------------------------------------------------------------------------------------------|
| invalid_request | 400 | 请求的格式错误。 |
| invalid_client | 403 | 不再允许客户端ID执行请求。 应生成新的客户端凭据。 |
| access_denied | 401 | access_token无效（过期或无效）。 客户端必须请求新的access_token。 |

### 执行身份验证请求示例：

**将访问令牌作为请求参数发送：**

```HTTPS
GET adobe-services/config?access_token=<access_token>&requestor_id=... HTTP/1.1
    
Host: sp.auth.adobe.com
```

**将访问令牌作为HTTP标头发送：**

```HTTPS
POST adobe-services/sessionDevice?device_id=platformDeviceId HTTP/1.1
    
Authorization: Bearer <access_token>
    
Host: sp.auth.adobe.com
```

**错误响应作为响应正文：**

```HTTPS
HTTP/1.1 401 Unauthorized
Content-Type: application/json;charset=UTF-8
Cache-Control: no-store
Pragma: no-cache
    
{ "error":"invalid_client" }
```

**作为URL参数响应错误：**

```HTTPS
HTTP/1.1 302 Found
    
Location: adobepass://com.programmer.adobe?error=access_denied
```
