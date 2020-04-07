---
description: 您可以使用TVSDK在Cookie标头中发送任意数据，以进行会话管理、门访问等。
seo-description: 您可以使用TVSDK在Cookie标头中发送任意数据，以进行会话管理、门访问等。
seo-title: 使用Cookie
title: 使用Cookie
uuid: 618bc59a-032d-445e-a867-ed2bf260570d
translation-type: tm+mt
source-git-commit: 5ada8632a7a5e3cb5d795dc42110844244656095

---


# 使用Cookie {#work-with-cookies}

您可以使用TVSDK在Cookie标头中发送任意数据，以进行会话管理、门访问等。

下面是对密钥服务器进行身份验证的示例请求：

1. 客户在浏览器中登录您的网站，其登录表明允许此客户视图内容。
1. 根据许可证服务器期望的内容，您的应用程序生成一个身份验证令牌。

   此值将传递给TVSDK。
1. TVSDK在cookie头中设置此值。
1. 当TVSDK向密钥服务器发出获取密钥以解密内容的请求时，该请求在cookie头中包含身份验证值。

   密钥服务器知道请求有效。

要使用Cookie，请执行以下操作：

1. 创建 `cookieManager` 并将URI的Cookie添加到cookieStore。

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

   TVSDK在运行 `cookieManager` 时查询它，检查是否有任何与URL关联的Cookie，并自动使用这些Cookie。

   如果在播放过程中需要在应用程序中更新Cookie，请不要使用 `networkConfiguration.setCookieHeaders` API，因为JAVA Cookie存储中会发生更新。

   `networkConfiguration.setCookieHeaders` API将cookies设置为TVSDK的C++ CookieStore。

   使用JAVA cookies并在应用程序和TVSDK之间共享它们时，请使用JAVA CookieStore仅管理cookies。

   在初始化播放之前，如上所述，使用Cookie管理器将cookies设置为CookieStore。

   TVSDK将自动获取存储在CookieStore中的Cookie。

   如果稍后在播放过程中需要更新Cookie值，请使用相同的键和新值字段调用CookieStore的相同添加方法。

   还设置
   `networkConfiguration.setReadSetCookieHeader`(false)在调用之前
   `config.setNetworkConfiguration(networkConfiguration)`

   >[!NOTE]
   >
   >将此“setReadSetCookieHeader”设置为false后，使用JAVA cookie管理器为密钥请求设置Cookie。

   `onCookiesUpdated(CookiesUpdatedEvent cookiesUpdatedEvent)`
只要C++ Cookies（来自http响应的cookie）中有更新，将触发此回调API。 应用程序需要侦听此回调并可相应更新其JAVA CookieStore，以便其JAVA网络调用可以如下利用Cookie:

   ```
   private final CookiesUpdatedEventListener cookiesUpdatedEventListener = new CookiesUpdatedEventListener() {
   @Override
   public void onCookiesUpdated(CookiesUpdatedEvent cookiesUpdatedEvent) {
   List<HttpCookie> cookies = cookiesUpdatedEvent.getHttpCookies();
   for(int i = 0; i < cookies.size(); i++)
   { HttpCookie c = cookies.get(i); // To set this cookie on to the cookie store //c.setValue("newValue"); //If you want to modify the value of the cookie URI myuri = URI.create(cookiesUpdatedEvent.getDomainString()); cookieManager.getCookieStore().add(myuri,c); }
   }
   }
   ```
