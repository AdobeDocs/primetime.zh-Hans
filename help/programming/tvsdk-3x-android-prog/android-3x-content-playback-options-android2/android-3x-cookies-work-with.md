---
description: 您可以使用TVSDK在Cookie标头中发送任意数据，以进行会话管理、网关访问等。
title: 使用Cookie
exl-id: 7f0e7d77-0718-4df7-8380-0e9351f588bc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# 使用Cookie {#work-with-cookies}

您可以使用TVSDK在Cookie标头中发送任意数据，以进行会话管理、网关访问等。

以下是向密钥服务器发出的一些身份验证请求示例：

1. 您的客户在浏览器中登录到您的网站，其登录信息显示允许该客户查看内容。
1. 您的应用程序会根据许可证服务器的预期生成一个身份验证令牌。

   此值将传递到TVSDK。
1. TVSDK会在Cookie标头中设置此值。
1. 当TVSDK向密钥服务器发出获取密钥以解密内容的请求时，该请求在Cookie标头中包含身份验证值。

   密钥服务器知道该请求有效。

要使用Cookie，请执行以下操作：

1. 创建 `cookieManager` 并将URI的Cookie添加到CookieStore。

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
   >启用302重定向后，广告请求可能会被重定向到与Cookie所属的域不同的域。

   TVSDK对此进行查询 `cookieManager` 在运行时，检查是否存在与该URL关联的任何Cookie，并自动使用这些Cookie。

   如果在播放期间需要更新应用程序中的Cookie，请不要使用 `networkConfiguration.setCookieHeaders` 作为更新的API将出现在JAVA Cookie存储中。

   `networkConfiguration.setCookieHeaders` API将Cookie设置为TVSDK的C++ CookieStore。

   使用JAVA Cookie并在应用程序和TVSDK之间共享它们时，请使用JAVA CookieStore单独管理Cookie。

   在初始化播放之前，使用Cookie管理器将Cookie设置为CookieStore，如上所述。

   TVSDK将自动提取存储在CookieStore中的Cookie。

   如果需要稍后在播放期间更新Cookie值，请使用相同的键和一个新的值字段调用CookieStore的相同add方法。

   也设置
   `networkConfiguration.setReadSetCookieHeader`(false)之前调用
   `config.setNetworkConfiguration(networkConfiguration)`

   >[!NOTE]
   >
   >将此“setReadSetCookieHeader”设置为false后，请使用JAVA Cookie管理器设置关键请求的Cookie。

   `onCookiesUpdated(CookiesUpdatedEvent cookiesUpdatedEvent)`
每当C++ Cookie（来自http响应的Cookie）中有更新时，都会触发此回调API。 应用程序需要侦听此回调，并且可以相应地更新其JAVA CookieStore，以便他们在JAVA中的网络调用可以使用Cookie，如下所示：

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
