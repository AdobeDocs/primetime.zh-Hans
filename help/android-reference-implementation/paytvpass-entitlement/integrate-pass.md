---
description: 自定义您的参考实施，以便为您的生产环境集成Adobe Primetime身份验证。
title: 集成Primetime身份验证
exl-id: ef6dc75d-d00f-481f-a620-4ec402cbebb6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 0%

---

# 集成Primetime身份验证 {#integrate-primetime-authentication}

自定义您的参考实施，以便为您的生产环境集成Adobe Primetime身份验证。

Primetime身份验证服务的引用实施集成可开箱即用作为演示。 但是，要在生产就绪的播放器中使用集成，您必须实施以下自定义设置：

1. 启用或禁用权利流。

   此 `EntitlementManager` 必须首先初始化并获取要启用的Primetime身份验证SDK实例。 如果 `EntitlementManager` 不初始化此库，将禁用管理器。
1. 启用 `EntitlementManger`，从主应用程序类中：

   ```java
   // initialize the AccessEnabler library, required for Primetime PayTV Pass entitlement workflows 
   EntitlementManager.initializeAccessEnabler(this); // comment out this line to disable entitlement workflows
   ```

1. 使用 `ManagerFactory` 类以获取的实例 `EntitlementManager`.

   您必须始终使用 `ManagerFactory` 以获取 `EntitlementManager`，作为 `ManagerFactory` 维护应用程序的单个EntitlementManager实例。 从不实例化 `EntitlementManager` 或 `EntitlementManagerOn` 类使用它们的构造函数。

   ```java
   EntitlementManager entitlementManager =  
   ManagerFactory.getEntitlementManager();
   ```

   此 `ManagerFactory` 返回实例 `EntitlementManagerOn`，并启用了权利流(如果您之前调用了 `EntitlementManager.initializeAccessEnabler`. 如果您不首先调用 `EntitlementManager.initializeAccessEnabler`，则 `ManagerFactory` 将返回实例 `EntitlementManager`，并禁用权利流。 1.配置请求者ID。

   参考实施中预先配置了测试请求者ID，并将其设置为：“REF”。 您可以使用此请求者ID来测试您的应用程序。 当您准备好使用Primetime身份验证代表提供给您的请求者ID时，请更新应用程序的 [!DNL res/values/strings.xml] 包含请求者ID的文件。

   ```xml
   <!-- Programmer Requestor ID, change to ID provided by your Adobe  
        Primetime pay-TV pass representative --> 
   <string name="adobepass_requestor_id">REF</string> 
   
   <!-- Adobe Primetime pay-TV pass service provider endpoint for production 
        environment --> 
   <string name="adobepass_sp_url_production">sp.auth.adobe.com</string> 
   
   <!-- Adobe Primetime pay-TV pass service provider endpoint for staging  
        environment --> 
   <string name="adobepass_sp_url_staging">sp.auth-staging.adobe.com</string>
   ```

   此外，您可能需要更改应用程序用于连接到Primetime身份验证服务的URL。 其中包括Primetime身份验证暂存和生产服务器URL，以及令牌验证服务的URL。 有关详细信息，请咨询您的Adobe Primetime代表。 1.签署请求者ID。

   为了在Primetime认证系统中建立程序员的身份，将程序员的请求者ID发送到Primetime认证系统。 作为附加的安全层，请求者ID在发送给Adobe之前必须由程序员签名。 Adobe建议程序员设置一项服务，以便在受信任网络上签署请求者ID。

   Primetime参考实施演示了如何对请求者ID进行签名，但这仅用于演示目的。 Adobe强烈建议签名证书和签名生成器代码位于 `com.adobe.primetime.reference.crypto`、不应包含在生产应用程序中。 相反，您应该将其移动到受信任的网络服务。

1. 配置服务器环境。

   Primetime身份验证服务可以在两个不同的环境中运行：

   * 暂存 — 暂存环境用于测试应用程序。
   * 生产 — 生产环境用于应用程序的实时部署。

   您可使用应用程序为暂存环境和生产环境设置URI，但您必须在代码中设置应用程序使用哪些URI。 在 `com.adobe.primetime.reference.manager.EntitlementManger` 类，设置 `environmentUri` 变量更改为 `STAGING_URI` 或 `PRODUCTION_URI` 根据您使用的Primetime身份验证服务环境。

   >[!NOTE]
   >
   >提供的请求者ID(“REF”)应仅用于暂存环境。

   `com.adobe.primetime.reference.manager.EntitlementManager`:

   ```java
     // Adobe Primetime authentication service provider endpoint for production environment 
     PRODUCTION_URI = 
         application.getResources().getString(R.string.adobepass_sp_url_production); 
   
     // Adobe Primetime authentication service provider endpoint for staging environment 
     STAGING_URI = 
       application.getResources().getString(R.string.adobepass_sp_url_staging); 
   
     // Set to STAGING_URI when testing against the staging/test environment 
     // Set to PRODUCTION_URI when deploying the application for production use 
     String environmentUri = STAGING_URI; 
   
     // Adobe Primetime authentication service URI used by this application 
     PAYTV_PASS_URI = environmentUri + "/adobe-services"; 
   
     // Token Verification Service URL 
     TVS_URL = "https://" + environmentUri + "/tvs/v1/validate";
   ```

1. 自定义MVPD选择网格。

   “内容提供方选择”页显示了用户可选择的前九个MVPD的表。 应用程序从应用程序内的有序列表中提取前九个MVPD，这些有序列表与Primetime身份验证系统中与程序员集成的可用MVPD匹配。 主MVPD的有序列表在Primetime身份验证系统内的MVPD ID上键入，而不是MVPD显示名称。 验证主MVPD列表中的MVPD ID是否与与与程序员帐户集成的MVPD ID匹配很重要，因为在某些情况下，ID在集成中可能不同。 以下是在类中找到的主要MVPD的排序列表 `com.adobe.primetime.reference.ui.entitlement.MvpdPickerFragment`.

   ```java
   /* Array of MVPDs to display in a Grid of icons 
   When displaying a grid, only the MVPDs which intersect this array and the 
   ArrayList of all MVPDs are displayed. 
   The array contents are ordered by display preference as only a maximum of 
   MAX_DISPLAY_ICONS are displayed. 
   */ 
   private static final String[] PRIMARY_MVPDS = { 
   "Comcast_SSO",                         // Comcast XFINITY 
   "DTV",                                 // DirectTV 
   "Dish",                                // Dish 
   "TWC",                                 // Time Warner Cable 
   "Cox",                                 // Cox 
   "Charter_Direct",                      // Charter 
   "Verizon",                             // Verizon FiOS 
   "Cablevision",                         // Cablevision Optimum 
   "ATT",                                 // AT&T U-verse 
   "Brighthouse",                         // Brighthouse 
   "Suddenlink",                          // Suddenlink 
   "Mediacom",                            // Mediacom 
   "CableOne",                            // CableOne 
   "WOW",                                 // WOW! 
   "RCN",                                 // RCN 
   "auth_atlanticbb_net",                 // Atlantic Broadband 
   "auth_armstrongmywire_com",            // Armstrong 
   "knology_auth-gateway_net",            // KNOLOGY 
   "serviceelectric_auth-gateway_net",    // Service Electric Cablevision 
   "msauth_midco_net",                    // Midcontinent Communications 
   "auth_metrocast_net",                  // MetroCast 
   "www_websso_mybrctv_com",              // Blue Ridge Communications 
   };
   ```

   下表提供了如何使用主MVPD的排序列表的示例。 第一列列出了与程序员集成的MVPD。 第二列是MVPD的（缩短的）排序列表。 第三列是用来向用户显示前六个MVPD的结果列表。

   此示例使用前六个MVPD而不是实际的9个，以简化示例。 请注意结果列表如何包含前两个列表的交集，并且其顺序与第二个列表相同。 此外，请注意AT&amp;T U版本不在最终列表中，因为只选择了第一个匹配的6个MVPD。

| 可用MVPD | 主MVPD | 显示了6个MVPD |
|--- |--- |--- |
| <ol><li>Comcast XFINITY</li><li>TWC</li><li>Mediacom</li><li>RCN</li><li>菜肴</li><li>AT&amp;T反向</li><li>CableOne</li><li>Brighthouse</li><li>大西洋宽带</li><li>哇！</li><li>MetroCast</li><li>Directv </li><li>考克斯</li><li>Cablevision Optimum</li></ol> | <ol><li>Comcast XFINITY</li><li>Directv</li><li>菜肴</li><li> TWC</li><li>考克斯</li><li>宪章</li><li>Verizon FiOS</li><li>Cablevision Optimum</li><li>AT&amp;T反向</li></ol> | <ol><li>Comcast XFINITY</li><li>Directv</li><li>菜肴</li><li>TWC</li><li>考克斯</li><li>Cablevision Optimum</li></ol> |
