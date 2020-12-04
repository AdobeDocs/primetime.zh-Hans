---
description: 您可以使用TVSDK在Cookie标头中发送任意数据以进行会话管理、进行门访问等。
seo-description: 您可以使用TVSDK在Cookie标头中发送任意数据以进行会话管理、进行门访问等。
seo-title: 使用Cookie
title: 使用Cookie
uuid: a3b966fd-1263-458d-8303-b4e898372ee1
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---


# 使用Cookie{#work-with-cookies}

您可以使用TVSDK在Cookie标头中发送任意数据以进行会话管理、进行门访问等。

下面是对密钥服务器进行验证的示例请求：

1. 客户在浏览器中登录您的网站，其登录表明允许此客户视图内容。
1. 根据许可证服务器的预期，您的应用程序将生成一个身份验证令牌。

   此值将传递给TVSDK。
1. TVSDK在cookie头中设置此值。
1. 当TVSDK向密钥服务器请求获取密钥以解密内容时，该请求在cookie头中包含身份验证值。

   密钥服务器知道请求有效。

要使用Cookie:

创建`cookieManager`，并将URI的cookie添加到cookieStore。

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
>启用302重定向后，广告请求可被重定向到不同于cookie所属域的域。

TVSDK在运行时查询此`cookieManager`，检查是否有任何与URL关联的cookie，并自动使用这些cookie。

更新C++ Cookie时将调用事件MediaPlayerEvent.COOKIES_UPDATED。 此cookiesUpdatedEvent有一个方法getCookieString()，它为cookie返回字符串值。

示例代码片段如下：

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

