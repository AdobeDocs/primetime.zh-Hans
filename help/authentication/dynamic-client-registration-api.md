---
title: 动态客户端注册API
description: 动态客户端注册API
exl-id: 06a76c71-bb19-4115-84bc-3d86ebcb60f3
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---

# 动态客户端注册API {#dynamic-client-registration-api}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权的使用。

## 概述 {#overview}

目前，Primetime身份验证有两种方式来标识和注册应用程序：

* 基于浏览器的客户端是通过“允许”进行注册 [域列表](/help/authentication/programmer-overview.md)
* 本机应用程序客户端(如iOS和Android应用程序)通过签名的请求者机制进行注册。

Adobe Primetime身份验证提出了一种注册应用程序的新机制。 以下各段介绍了这一机制。

## 申请注册机制 {#appRegistrationMechanism}

### 技术原因 {#reasons}

Adobe Primetime身份验证中的身份验证机制依赖于会话Cookie，但原因在于 [Android Chrome自定义选项卡](https://developer.chrome.com/multidevice/android/customtabs){target=_blank} and [Apple Safari View Controller](https://developer.apple.com/documentation/safariservices/sfsafariviewcontroller){target=_blank}，此目标无法再实现。

鉴于这些限制，Adobe为所有客户引入了新的注册机制。 它基于OAuth 2.0 RFC并包含以下步骤：

1. 从TVE仪表板检索软件语句
1. 获取客户端凭据
1. 获取访问令牌

### 从TVE仪表板检索软件语句 {#softwareStatement}

对于您发布的每个应用程序，都需要获取一份软件声明。 创建应用程序后，所有软件语句都将通过TVE仪表板提供。 软件语句应该与用户设备上的应用程序一起部署。

>[!IMPORTANT]
>
>使用软件语句时，不再需要使用已签名的请求者ID机制。

有关如何创建软件语句的更多详细信息，请访问 [TVE仪表板中的客户端注册](/help/authentication/dynamic-client-registration.md).

### 获取客户端凭据 {#clientCredentials}

从TVE仪表板检索软件语句后，您需要向Adobe Primetime授权服务器注册应用程序。 要执行此操作，请执行/register调用并检索您的唯一客户端标识符。

**请求**

| HTTP调用 |  |
|-----------|--------------------|
| 路径 | /o/client/register |
| 方法 | POST |

| 字段 |  |  |
|--------------------|---------------------------------------------------------------------------|-----------|
| software_statement | 在TVE Dashboard中创建的软件语句。 | 必需 |
| redirect_uri | 应用程序用于完成身份验证流程的URI。 | 可选 |

| 请求标头 |  |  |
|-----------------|--------------------------------------------------------------------------------|-----------|
| 内容类型 | application/json | 必需 |
| X-Device-Info | 传递设备和连接信息中定义的设备信息 | 必需 |
| 用户代理 | 用户代理 | 必需 |

**响应**

| 响应标头 |  |  |
|------------------|------------------|-----------|
| 内容类型 | application/json | 必需 |

| 响应字段 |  |  |
|---------------------|-----------------|----------------------------|
| client_id | 字符串 | 必需 |
| client_secret | 字符串 | 必需 |
| client_id_issued_at | 长 | 必需 |
| redirect_uris | 字符串列表 | 必需 |
| grant_types | 字符串列表<br/> **接受值**<br/> `client_credentials`：由不安全的客户端使用，例如Android SDK。 | 必需 |
| 错误 | **接受的值**<ul><li>invalid_request</li><li>invalid_redirect_uri</li><li>invalid_software_statement</li><li>unapproved_software_statement</li></ul> | 错误流中的必需项 |


#### 错误响应 {#error-response}

如果出现错误，注册服务器将使用HTTP 400（错误请求）状态代码进行响应，并在响应中包含以下参数：

| 状态代码 | 响应正文 | 描述 |
| --- | --- | --- |
| HTTP 400 | {&quot;error&quot;： &quot;invalid_request&quot;} | 请求缺少必需的参数、包含不受支持的参数值、重复某个参数或格式不正确。 |
| HTTP 400 | {&quot;error&quot;： &quot;invalid_redirect_uri&quot;} | 根据此客户端注册的应用程序，不允许对该客户端使用redirect_uri。 |
| HTTP 400 | {&quot;error&quot;： &quot;invalid_software_statement&quot;} | 软件语句无效。 |
| HTTP 400 | {&quot;error&quot;： &quot;unapproved_software_statement&quot;} | 在配置中找不到software_id。 |

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

在检索应用程序的唯一客户端标识符（客户端ID和客户端密钥）后，您需要获取访问令牌。 访问令牌是必需的OAuth 2.0令牌，用于调用Primetime身份验证API。

>[!NOTE]
>
>目前，访问令牌的生存时间为24小时。

**请求**


| **HTTP调用** |  |
| --- | --- |
| 路径 | `/o/client/token` |
| 方法 | POST |

| **请求参数** |  |
| --- | --- |
| `grant_type` | 在客户端注册过程中接收。<br/> **接受的值**<br/>`client_credentials`：用于不安全的客户端，例如Android SDK。 |
| `client_id` | 在客户端注册过程中获取的客户端标识符。 |
| `client_secret` | 在客户端注册过程中获取的客户端标识符。 |

**响应**

| 响应字段 |  |  |
| --- | --- | --- |
| `access_token` | 您应该用于调用Primetime API的访问令牌值 | 必需 |
| `expires_in` | access_token过期之前的秒数 | 必需 |
| `token_type` | 令牌的类型 **载体** | 必需 |
| `created_at` | 令牌的问题时间 | 必需 |
| **响应标头** |  |  |
| `Content-Type` | application/json | 必需 |

**错误响应**

如果出现错误，授权服务器将使用HTTP 400（错误请求）状态代码进行响应，并在响应中包含以下参数：

| 状态代码 | 响应正文 | 描述 |
| --- | --- | --- |
| HTTP 400 | {&quot;error&quot;： &quot;invalid_request&quot;} | 请求缺少必需的参数，包括不受支持的参数值（授权类型除外），重复参数，包括多个凭据，使用多个机制来验证客户端，或者格式不正确。 |
| HTTP 400 | {&quot;error&quot;： &quot;invalid_client&quot;} | 客户端身份验证失败，因为客户端未知。 SDK必须再次向授权服务器注册。 |
| HTTP 400 | {&quot;error&quot;： &quot;unauthorized_client&quot;} | 经过身份验证的客户端无权使用此授权授予类型。 |

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

使用访问令牌执行Adobe Primetime [身份验证API调用](/help/authentication/initiate-authentication.md). 为此，需要通过以下方式之一将访问令牌添加到API请求中：

* 向请求中添加新的查询参数。 该新参数名为 **access_token**.

* 通过向请求添加新的HTTP标头： Authorization： Bearer。 我们建议您使用HTTP标头，因为查询字符串往往显示在服务器日志中。

如果出现错误，可能会返回以下错误响应：

| 错误响应 |  |  |
|-----------------|-----|--------------------------------------------------------------------------------------------------------|
| invalid_request | 400 | 请求的格式不正确。 |
| invalid_client | 403 | 不再允许客户端ID执行请求。 应生成新的客户端凭据。 |
| access_denied | 401 | access_token无效（已过期或无效）。 客户端必须请求新的access_token。 |

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

**错误响应作为URL参数：**

```HTTPS
HTTP/1.1 302 Found
    
Location: adobepass://com.programmer.adobe?error=access_denied
```
