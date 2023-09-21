---
description: 您可以使用TVSDK在Cookie标头中发送任意数据，以进行会话管理、网关访问等。
title: 使用Cookie
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# 使用Cookie {#work-with-cookies}

您可以使用TVSDK在Cookie标头中发送任意数据，以进行会话管理、网关访问等。

以下是向密钥服务器发出的一些身份验证请求示例：

1. 您的客户在浏览器中登录到您的网站，其登录信息显示该客户有权查看内容。
1. 您的应用程序会根据许可证服务器的预期生成身份验证令牌。

   此值将传递到TVSDK。
1. TVSDK会在Cookie标头中设置此值。
1. 当TVSDK向密钥服务器发出获取密钥以解密内容的请求时，该请求在Cookie标头中包含身份验证值。

   密钥服务器知道请求有效。

要使用Cookie，请执行以下操作：

创建 `cookieManager` 并将URI的Cookie添加到CookieStore中。

例如：

```java
CookieManager cookieManager=new CookieManager(); 
CookieHandler.setDefault(cookieManager);  
HttpCookie cookie=new HttpCookie("lang","fr"); 
cookie.setDomain("twitter.com");  
cookie.setPath("/"); 
cookie.setVersion(0); 
cookieManager.getCookieStore().add(newURI("https://twitter.com/"),cookie);
```

>[!TIP]
>
>启用302重定向后，广告请求可能会重定向到与Cookie所属的域不同的域。

TVSDK查询此 `cookieManager` 在运行时，检查是否存在与该URL关联的任何Cookie，并自动使用这些Cookie。

更新C++ Cookie时，将调用MediaPlayerEvent.COOKIES_UPDATED事件。 此cookiesUpdatedEvent具有方法getCookieString()，可返回Cookie的字符串值。

下面是一个示例代码段：

```
private final CookiesUpdatedEventListener cookiesUpdatedEventListener = new CookiesUpdatedEventListener()  
{ 
@Override 
public void onCookiesUpdated(CookiesUpdatedEvent cookiesUpdatedEvent) 
 { 
 String cookieStr = cookiesUpdatedEvent.getCookieString();  
 logger.i(LOG_TAG + "::MediaPlayer.CookiesUpdatedEventListener#onCookiesUpdated()", "cookieStr " + cookieStr);  
 }  
};
```
