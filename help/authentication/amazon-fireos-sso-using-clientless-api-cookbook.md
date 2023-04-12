---
title: Amazon FireOS单点登录（使用无客户端API指南）
description: Amazon FireOS单点登录（使用无客户端API指南）
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 0%

---


# Amazon FireOS单点登录（使用无客户端API指南） {#amazon-fireos-sso-using-clientless-api-cookbook}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

</br>

## 简介 {#Introduction}

本文档提供了使用无客户端API实施Amazon SSO版本的Adobe Primetime身份验证流程的说明。 本文件的第一部分重点介绍Amazon版体系结构的特点，对于许多已经熟悉并经验丰富的合作伙伴而言。

文档的第二部分将介绍实施Adobe Primetime Authentication无客户端API的主要步骤。

有关无客户端解决方案工作原理的广泛技术概述，请参阅 [REST API概述](/help/authentication/rest-api-overview.md). Adobe是支持整体架构和首次实施的首选联系人。

## Amazon无客户端单点登录 {#AMZ-Clientless-SSO}

### 高级架构 {#High-Level-Arch}

Amazon无客户端SSO实施非常简单，并且与常规的Adobe Primetime无客户端身份验证API基本相同。

您将需要使用Amazon SDK检索个性化的有效负载，并在调用Adobe无客户端API时使用它。

如果有效负载被识别并与已验证的会话相对应，则无客户端API将随会话的令牌立即返回。

### 如何构建应用程序以使用Amazon SDK {#Build-entries}

* 下载并复制最新版本 [Amazon Stub SDK](https://tve.zendesk.com/hc/en-us/article_attachments/360064368131/ottSSOTokenLib_v1.jar) 到与应用程序目录平行的/SSOEnabler文件夹中
* 更新清单/Gradle文件以使用库：

   **将以下行添加到清单文件：**

   ```Java
   <uses-library android:name="com.amazon.ottssotokenlib" android:required="false"/\>
   ```

   **Gradle文件条目：**

   在存储库下：

   ```java
   flatDir {
        dirs '../SSOEnabler'
   }
   ```

   在依赖关系下，添加：

   ```Java
   provided fileTree(include: \['ottSSOTokenStub.jar'\], dir: '../SSOEnabler')
   ```


* 处理缺少Amazon配套应用程序的问题：

   虽然不太可能，但是如果您的应用程序正在运行的Amazon设备上不存在该伴随，您应该在以下类的运行时遇到ClassNotFoundException: `com.amazon.ottssotokenlib.SSOEnabler`.

   如果发生这种情况，您只需跳过有效负载步骤并返回常规PrimeTime流。 未启用SSO，但将正常执行常规身份验证流程。

</br>

### 如何使用Amazon SDK获取Amazon SSO有效负载 {#UseAmazonSSO}

在应用程序初始化期间，获取SSOEnabler的实例。 根据您的应用程序架构，您应该决定是同步实施还是异步实施。

如果由于任何原因，API调用不返回有效负载，请使用常规的非单点登录流程并联系您的Amazon和Adobe合作伙伴进行调查。

**异步API**

* 获取SSO启用程序实例：

   ```Java
   ssoEnabler = SSOEnabler.getInstance(context);
   SSOEnablerCallback ssoEnablerCallback = new SSOEnablerCallbackImpl();
   ssoEnabler.setSSOTokenCallback(ssoEnablerCallback);
   ```


* 设置回调 

   ```java
   public static abstract class SSOEnablerCallback
   {
           public abstract void getSSOTokenSuccess(Bundle result);
           public abstract void getSSOTokenFailure(Bundle result);
   }
   ```

   * 成功响应包将包含：
      * SSO令牌，作为键为“SSOToken”的字符串
   * 失败响应包将包含：
      * 错误代码作为键为“ErrorCode”的int
      * 错误描述为键为“ErrorDescription”的字符串


* 获取SSO令牌

   ```JAVA
   Bundle getSSOTokenAsync(Void);
   ```

* 此API将在初始化期间通过回调集提供响应。

   **Ex**. 使用在初始化期间创建的singleton实例调用：

   ```JAVA
   ssoEnabler.getSSOTokenAsync().
   ```


**同步API**

* 获取SSO启用程序实例并设置回调

   ```JAVA
   ssoEnabler = SSOEnabler.getInstance(context);</span>
   ```

* 获取SSO令牌

   ```JAVA
   Bundle getSSOTokenSync(Void);
   ```

   * 此API将阻止调用方线程，并使用结果包做出响应。 由于这是同步调用，请确保不要在主线程中使用它。

   ```JAVA
   void setSSOTokenTimeout(long);
   ```

   * 值（以毫秒为单位）。 如果设置，则覆盖同步API的默认超时值1分钟。



### Adobe Primetime无客户端API更新以使用动态客户端注册 {#clientlessdcr}

如果这是您的第一个实施，请参阅 **无客户端技术概述** 如果您需要支持，请联系Adobe。

Adobe无客户端API要求应用程序使用动态客户端注册，以便调用Adobe服务器。

* 要在您的应用程序中使用动态客户端注册，请按照 [ Dynamic Client Registration Management注册应用程序](/help/authentication/dynamic-client-registration-management.md).

* 要实施Dynamic Client Registration API以对Adobe Primetime服务器执行身份验证和授权请求，请按照 [动态客户端注册API](/help/authentication/dynamic-client-registration-api.md) .

### Adobe Primetime无客户端API更新以使用Amazon SSO {#clientlesssso}

从Amazon SDK获取的Amazon SSO有效负载需要存在于对Adobe Primetime身份验证端点发出的请求中：

```
      /adobe-services/*
      /reggie/*
      /api/*
```


所有Primetime身份验证端点都支持以下方法来接收设备范围标识符或平台范围标识符(在Amazon SSO有效负载中存在):

* 作为标题：&quot;Adobe主体令牌&quot;
* 作为查询参数：&quot;ast&quot;
* 作为帖子参数：&quot;ast&quot;


>[!NOTE]
>
>如果设备范围标识符或平台范围标识符作为查询/后处理参数发送，则在生成请求签名时必须包含该标识符。

>[!NOTE]
>
>使用查询参数“ast”，整个URL可能会变得非常长且会被拒绝。 在/authenticate调用中，可以跳过此参数，因为它是在/regcode调用中提供的

**示例：**

**作为自定义标头发送**

```HTTPS
GET /adobe-services/config/requestor HTTP/1.1 Host: sp-preprod.auth.adobe.com

Adobe-Subject-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJyb2t1IiwiaWF0IjoxNTExMzY4ODAyLCJleHAiOjE1NDI5MDQ4MDIsImF1ZCI6ImFkb2JlIiwic3ViIjoiNWZjYzMwODctYWJmZi00OGU4LWJhZTgtODQzODViZTFkMzQwIiwiZGlkIjoiY2FmZjQ1ZDAtM2NhMy00MDg3LWI2MjMtNjFkZjNhMmNlOWM4In0.JlBFhNhNCJCDXLwBjy5tt3PtPcqbMKEIGZ6sr2NA
```

**作为查询参数发送**

```HTTPS
GET /adobe-services/config/requestor?ast=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJyb2t1IiwiaWF0IjoxNTExMzY4ODAyLCJleHAiOjE1NDI5MDQ4MDIsImF1ZCI6ImFkb2JlIiwic3ViIjoiNWZjYzMwODctYWJmZi00OGU4LWJhZTgtODQzODViZTFkMzQwIiwiZGlkIjoiY2FmZjQ1ZDAtM2NhMy00MDg3LWI2MjMtNjFkZjNhMmNlOWM4In0.JlBFhNhNCJCDXLwBjy5tt3PtPcqbMKEIGZ6sr2NA

HTTP/1.1
Host: sp.auth.adobe.com
```


**作为帖子参数发送**


```HTTPS
POST /adobe-services/config/requestor?ast=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJyb2t1IiwiaWF0IjoxNTExMzY4ODAyLCJleHAiOjE1NDI5MDQ4MDIsImF1ZCI6ImFkb2JlIiwic3ViIjoiNWZjYzMwODctYWJmZi00OGU4LWJhZTgtODQzODViZTFkMzQwIiwiZGlkIjoiY2FmZjQ1ZDAtM2NhMy00MDg3LWI2MjMtNjFkZjNhMmNlOWM4In0.Jl\_BFhN\_h\_NCJCDXLwBjy5tt3PtPcqbMKEIGZ6sr2NA

HTTP/1.1
Host: sp.auth.adobe.com Content-Type: multipart/form-data;
boundary=---- WebKitFormBoundary7MA4YWxkTrZu0gW
```

>[!NOTE]
>
>如果Amazon SSO不存在或无效，Adobe Primetime身份验证将忽略该属性，并且将像SSO不存在一样执行调用。
