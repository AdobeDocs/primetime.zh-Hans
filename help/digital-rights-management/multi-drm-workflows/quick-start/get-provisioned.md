---
description: 要开始使用由ExpressPlay提供支持的Primetime DRM Cloud，您需要在Adobe代表的帮助下设置Adobe证书和ExpressPlay帐户。
seo-description: 要开始使用由ExpressPlay提供支持的Primetime DRM Cloud，您需要在Adobe代表的帮助下设置Adobe证书和ExpressPlay帐户。
seo-title: 设置（帐户等）
title: 设置（帐户等）
uuid: 51b95676-2121-4d8b-8756-9fd097185a13
translation-type: tm+mt
source-git-commit: 9792aff8586c46aabb5bfb70864cfe98c28e602d
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---


# 获取配置（帐户等）{#get-provisioned-accounts-etc}

要开始使用由ExpressPlay提供支持的Primetime DRM Cloud，您需要在Adobe代表的帮助下设置Adobe证书和ExpressPlay帐户。

1. 联系您的Adobe代表并请求Adobe证书和ExpressPlay帐户，以便通过TVSDK实施多DRM。

       向Adobe代表提供您将用作联系点的电子邮件地址。Adobe然后为您创建两个帐户：
   
   * ***证书门户帐户*** -(<span></span>https://certportal.primetime.adobe.com):Adobe *访问/Primetime DRM证书登记管理小* 组会向您提供的地址发送电子邮件。该电子邮件包含Adobe证书门户的URL，以及指向Adobe证书注册文档的链接(最新文档在此处：[证书注册指南](../../../digital-rights-management/certificate-enrollment-guide/about-certs.md))。

   * ***ExpressPlay帐户*** -Adobe会向您发送一封电子邮件，其中包含用于注册ExpressPlay管理员帐户的链接。

1. 使用您的Adobe ID登录Adobe证书门户(使用您提供给Adobe代表的相同电子邮件地址)。 如果您还没有Adobe ID，可以按照证书门户中的&#x200B;*获取Adobe ID*&#x200B;链接快速创建一个：

   <!--<a id="fig_mst_gtj_wv"></a>-->

   ![](assets/cert_portal_sign-in-page-web.png)

1. 在Adobe证书门户上，请求&#x200B;*试用*&#x200B;证书。

   对于多DRM试用版，单个试用证书将涵盖内容保护的所有这些方面：包装、许可和运输。 您需要提供您自己的[CSR](../../../digital-rights-management/certificate-enrollment-guide/request-certs/gen-cert-signing-req.md)来请求证书：
   <!--<a id="fig_op1_xwj_wv"></a>-->

   ![](assets/cert_portal_trial_request-web.png)

   Adobe将向您发送一封电子邮件，指示您接受或拒绝证书请求。 您可以在证书门户的&#x200B;*请求历史记录*&#x200B;选项卡上查看证书请求的状态：
   <!--<a id="fig_gkl_myj_wv"></a>-->

   ![](assets/cert_portal_request_history-web.png)

1. 创建您的ExpressPlay管理员帐户。

   按照链接操作，访问Adobe提供给您的ExpressPlay。 这将打开ExpressPlay上的&#x200B;*创建帐户*&#x200B;页面。 填写所需信息并提交表单。 您将收到一封来自`operations@expressplay.com`的电子邮件，其中包含一个激活链接，该链接为一周。 激活后，设置ExpressPlay服务：
   <!--<a id="fig_cjl_ztk_wv"></a>-->

   ![](assets/expressplay_create_service-web.png)

   创建服务后，将显示您自己的“管理员”页面。 除了某些活动跟踪字段外，您还将看到您的生产和测试&#x200B;*客户身份验证器*（API密钥）以及您的生产和测试服务URL:

   <!--<a id="fig_c5h_xdl_wv"></a>-->

   ![](assets/expressplay_admin_dashboard_2-web.png) ![](assets/expressplay_admin_dashboard-web.png)

1. 如果您使用FairPlay，则需要执行其他步骤（在Apple开发人员站点上）来设置ExpressPlay。 有关说明，请参阅[为FairPlay启用ExpressPlay服务](../../multi-drm-workflows/p-l-and-p/fairplay-workflow.md#enable-expressplay-service-for-fairplay)。
