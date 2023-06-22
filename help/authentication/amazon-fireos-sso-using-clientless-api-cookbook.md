---
title: 使用无客户端API指南的Amazon FireOS SSO
description: 使用无客户端API指南的Amazon FireOS SSO
exl-id: 4c65eae7-81c1-4926-9202-a36fd13af6ec
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 0%

---

# 使用无客户端API指南的Amazon FireOS SSO {#amazon-fireos-sso-using-clientless-api-cookbook}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权的使用。

</br>

## 介绍 {#Introduction}

本文档提供了使用无客户端API实施Amazon SSO版本的Adobe Primetime身份验证流的说明。 本文档的第一部分侧重于架构的Amazon版本的特性，适用于许多已经熟悉并熟悉其实施的合作伙伴。

本文档的第二部分介绍了实施Adobe Primetime身份验证无客户端API的主要步骤。

有关无客户端解决方案的工作原理的广泛技术概述，请参阅 [REST API概述](/help/authentication/rest-api-overview.md). Adobe是获取有关整体架构和第一个实施支持的首选联系人。

## Amazon无客户端SSO {#AMZ-Clientless-SSO}

### 高级体系结构 {#High-Level-Arch}

Amazon无客户端SSO实施非常简单，并且大多与常规Adobe Primetime身份验证无客户端API相同。

您将需要使用Amazon SDK检索个性化有效负载，并在调用Adobe无客户端API时使用它。

如果有效负载被识别并且对应于经过身份验证的会话，则无客户端API将立即使用会话的令牌返回。

### 如何构建应用程序以使用Amazon SDK {#Build-entries}

* 下载并复制最新版本 [Amazon桩模块SDK](https://tve.zendesk.com/hc/en-us/article_attachments/360064368131/ottSSOTokenLib_v1.jar) 移入/SSOEnabler文件夹，与app目录平行
* 更新manifest/gradle文件以使用库：

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

   在依赖项下，添加：

   ```Java
   provided fileTree(include: \['ottSSOTokenStub.jar'\], dir: '../SSOEnabler')
   ```


* 处理Amazon配套应用程序缺失的问题：

   虽然不太可能，但如果该随附程序不存在于应用程序正在运行的Amazon设备上，则您应在运行时遇到以下类的ClassNotFoundException： `com.amazon.ottssotokenlib.SSOEnabler`.

   如果发生这种情况，您只需跳过有效负载步骤并回退常规PrimeTime流。 将不会启用SSO，但常规身份验证流程将正常进行。

</br>

### 如何使用Amazon SDK获取Amazon SSO有效负载 {#UseAmazonSSO}

在应用程序初始化过程中，获取SSOEnabler的实例。 根据您的应用程序体系结构，您应该决定是同步实施还是异步实施。

如果由于任何原因，API调用未返回有效负载，请使用常规非SSO流程并联系您的Amazon和Adobe合作伙伴进行调查。

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
      * SSO令牌作为带密钥“SSOToken”的字符串
   * 故障响应包将包含：
      * 错误代码作为int和键“ErrorCode”
      * 错误描述作为带有键“ErrorDescription”的字符串


* 获取SSO令牌

   ```JAVA
   Bundle getSSOTokenAsync(Void);
   ```

* 此API将通过在初始化期间设置的回调提供响应。

   **例如**. 使用在初始化期间创建的单一实例调用：

   ```JAVA
   ssoEnabler.getSSOTokenAsync().
   ```


**同步API**

* 获取SSO Enabler实例并设置回调

   ```JAVA
   ssoEnabler = SSOEnabler.getInstance(context);</span>
   ```

* 获取SSO令牌

   ```JAVA
   Bundle getSSOTokenSync(Void);
   ```

   * 此API将阻止调用方线程并使用结果包进行响应。 由于这是同步调用，请确保不要在主线程中使用它。

   ```JAVA
   void setSSOTokenTimeout(long);
   ```

   * 值（以毫秒为单位）。 如果设置，则覆盖同步API的默认超时值1分钟。



### 更新了Adobe Primetime无客户端API以使用动态客户端注册 {#clientlessdcr}

如果这是您的第一个实施，请参阅 **无客户端技术概述** 并在您需要支持时联系Adobe。

Adobe无客户端API要求应用程序使用Dynamic Client Registration来调用Adobe服务器。

* 要在应用程序中使用Dynamic Client Registration，请按照 [ 用于注册应用程序的动态客户端注册管理](/help/authentication/dynamic-client-registration-management.md).

* 要实施Dynamic Client Registration API以对Adobe Primetime服务器执行身份验证和授权请求，请按照 [动态客户端注册API](/help/authentication/dynamic-client-registration-api.md) .

### 更新了Adobe Primetime无客户端API以使用Amazon SSO {#clientlesssso}

向Amazon身份验证端点发出的请求需要存在从Amazon SDK获取的Adobe Primetime SSO有效负载：

```
      /adobe-services/*
      /reggie/*
      /api/*
```


所有Primetime身份验证端点都支持以下方法来接收设备范围标识符或平台范围标识符(存在于Amazon SSO有效负载中)：

* 作为标头：&quot;Adobe-Subject-Token&quot;
* 作为查询参数：&quot;ast&quot;
* 作为post参数：&quot;ast&quot;


>[!NOTE]
>
>如果设备范围标识符或平台范围标识符作为查询/帖子参数发送，则在生成请求签名时必须包含该标识符。

>[!NOTE]
>
>使用查询参数“ast”，整个URL可能会变得非常长并被拒绝。 在/authenticate调用中，可以跳过此参数，因为它是在/regcode调用中提供的

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


**作为post参数发送**


```HTTPS
POST /adobe-services/config/requestor?ast=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJyb2t1IiwiaWF0IjoxNTExMzY4ODAyLCJleHAiOjE1NDI5MDQ4MDIsImF1ZCI6ImFkb2JlIiwic3ViIjoiNWZjYzMwODctYWJmZi00OGU4LWJhZTgtODQzODViZTFkMzQwIiwiZGlkIjoiY2FmZjQ1ZDAtM2NhMy00MDg3LWI2MjMtNjFkZjNhMmNlOWM4In0.Jl\_BFhN\_h\_NCJCDXLwBjy5tt3PtPcqbMKEIGZ6sr2NA

HTTP/1.1
Host: sp.auth.adobe.com Content-Type: multipart/form-data;
boundary=---- WebKitFormBoundary7MA4YWxkTrZu0gW
```

>[!NOTE]
>
>如果Amazon SSO不存在或无效，Adobe Primetime身份验证将忽略该属性，并像SSO不存在一样执行调用。
