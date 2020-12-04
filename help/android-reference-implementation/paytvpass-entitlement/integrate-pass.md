---
description: 自定义您的参考实施，为您的生产环境集成Adobe Primetime身份验证。
seo-description: 自定义您的参考实施，为您的生产环境集成Adobe Primetime身份验证。
seo-title: 集成Primetime身份验证
title: 集成Primetime身份验证
uuid: 34cdf1da-261e-462c-a194-4fcb439e5dfb
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 0%

---


# 集成Primetime身份验证{#integrate-primetime-authentication}

自定义您的参考实施，为您的生产环境集成Adobe Primetime身份验证。

Primetime身份验证服务的参考实施集成现成即用演示。 但是，要在生产就绪型播放器中使用集成，必须实现以下自定义：

1. 启用或禁用授权流。

   `EntitlementManager`必须首先初始化并获取要启用的Primetime身份验证SDK的实例。 如果`EntitlementManager`未初始化此库，则将禁用管理器。
1. 从主应用程序类中启用`EntitlementManger`:

   ```java
   // initialize the AccessEnabler library, required for Primetime PayTV Pass entitlement workflows 
   EntitlementManager.initializeAccessEnabler(this); // comment out this line to disable entitlement workflows
   ```

1. 使用`ManagerFactory`类获取`EntitlementManager`的实例。

   您必须始终使用`ManagerFactory`获取`EntitlementManager`的实例，因为`ManagerFactory`会为您的应用程序维护EntitlementManager的单个实例。 绝不使用`EntitlementManager`或`EntitlementManagerOn`类的构造函数来实例化它们。

   ```java
   EntitlementManager entitlementManager =  
   ManagerFactory.getEntitlementManager();
   ```

   如果您以前调用过`EntitlementManager.initializeAccessEnabler`，则`ManagerFactory`将返回一个实例`EntitlementManagerOn`，并启用授权流。 如果不首先调用`EntitlementManager.initializeAccessEnabler`，则`ManagerFactory`将返回`EntitlementManager`的实例，并禁用授权流。 1.配置请求者ID。

   The Reference Implementation is preconfigured with test Requestor ID set to:“参考”。 您可以使用此请求者ID来测试您的应用程序。 当您准备好使用由Primetime身份验证代表提供给您的请求者ID时，请使用您的请求者ID更新应用程序的[!DNL res/values/strings.xml]文件。

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

   此外，您可能需要更改您的应用程序用来连接Primetime身份验证服务的URL。 这些URL包括Primetime身份验证分阶和生产服务器URL以及令牌验证服务的URL。 有关详细信息，请咨询您的Adobe Primetime代表。 1.签署申请人ID。

   为了在Primetime认证系统内建立节目编排者的身份，节目编排者请求者ID被发送至Primetime认证系统。 作为增加的安全层，在将请求者ID发送给Adobe之前，必须由程序员对其进行签名。 Adobe建议程序员在可信网络上设置服务以签署请求者ID。

   Primetime参考实施演示了如何签署请求者ID，但仅用于演示目的。 Adobe强烈建议在生产应用程序中不要包含签名证书和`com.adobe.primetime.reference.crypto`下的签名生成器代码。 相反，您应将其迁移到可信任的网络服务。

1. 配置服务器环境。

   Primetime身份验证服务可以在两个不同的环境中运行：

   * 暂存——暂存环境用于测试应用程序。
   * 生产——生产环境用于应用程序的实时部署。

   您使用应用程序为分阶和生产环境设置URI，但必须设置代码中的应用程序使用的URI。 在`com.adobe.primetime.reference.manager.EntitlementManger`类中，根据您使用的Primetime身份验证服务环境，将`environmentUri`变量设置为`STAGING_URI`或`PRODUCTION_URI`。

   >[!NOTE]
   >
   >提供的请求者ID(“REF”)只应与登台环境一起使用。

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

   内容提供者选择页显示用户可从中选择的前九个MVPD的表。 应用程序从应用程序内的有序列表中拉取前9个MVPD，该订单符合Primetime身份验证系统中与节目编排者集成的可用MVPD。 主MVPD的有序列表在Primetime身份验证系统内的MVPD ID上进行键控，而不是MVPD显示名称。 务必验证主MVPD列表中的MVPD ID是否与与程序员帐户集成的MVPD ID是否匹配，因为在某些情况下，ID在不同集成中可能不同。 以下是类`com.adobe.primetime.reference.ui.entitlement.MvpdPickerFragment`中的主MVPD的有序列表。

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

   下表提供了如何使用主MVPD的有序列表的示例。 第一列列表与程序员集成的MVPD。 第二列是MVPD的（缩短）有序列表。 第三列是用于向用户显示前六个MVPD的结果列表。

   此示例使用前6个MVPD而不是实际的9个MVPD来使示例保持简单。 请注意，结果列表如何包含前两个列表的交集，并且与第二个列表的排序相同。 此外，请注意，AT&amp;T U正文并未处于最终列表，因为只有首批匹配的6个MVPD才会使用。

| 可用的MVPD | 主MVPD | 显示6个MVPD |
|--- |--- |--- |
| <ol><li>Comcast XFINITY</li><li>TWC</li><li>Mediacom</li><li>RCN</li><li>碟</li><li>AT&amp;T U-verse</li><li>CableOne</li><li>Brighthouse</li><li>Atlantic Broadband</li><li>哇！</li><li>MetroCast</li><li>DirectTV </li><li>考克斯</li><li>Cablevision Optimum</li></ol> | <ol><li>Comcast XFINITY</li><li>DirectTV</li><li>碟</li><li> TWC</li><li>考克斯</li><li>宪章</li><li>Verizon FiOS</li><li>Cablevision Optimum</li><li>AT&amp;T U-verse</li></ol> | <ol><li>Comcast XFINITY</li><li>DirectTV</li><li>碟</li><li>TWC</li><li>考克斯</li><li>Cablevision Optimum</li></ol> |
