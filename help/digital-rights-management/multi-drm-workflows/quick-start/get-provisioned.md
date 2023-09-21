---
description: 要开始使用由ExpressPlay提供支持的Primetime DRM Cloud，您需要在Adobe代表的帮助下设置Adobe证书和ExpressPlay帐户。
title: 进行配置（帐户等）
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---

# 进行配置（帐户等） {#get-provisioned-accounts-etc}

要开始使用由ExpressPlay提供支持的Primetime DRM Cloud，您需要在Adobe代表的帮助下设置Adobe证书和ExpressPlay帐户。

1. 请联系您的Adobe代表，并请求您将TVSDK用于实施多DRM所需的AdobeCert和ExpressPlay客户。

   向您的Adobe代表提供您将用作联系点的电子邮件地址。 然后，Adobe会为您创建两个帐户：

   * ***证书门户帐户*** - ( https://certportal.primetime.adobe.com) ：和 *Adobe访问/Primetime DRM证书注册管理团队* 会向您提供的地址发送电子邮件。 该电子邮件包含Adobe证书门户的URL，以及指向Adobe证书注册文档的链接(此处为最新文档： [证书注册指南](../../../digital-rights-management/certificate-enrollment-guide/about-certs.md))。

   * ***ExpressPlay帐户*** -Adobe向您发送一封电子邮件，其中包含用于注册ExpressPlay管理员帐户的链接。

1. 使用您的Adobe ID登录Adobe证书门户(使用您向Adobe代表提供的相同电子邮件地址)。 如果您还没有Adobe ID，则可以按照以下步骤快速创建一个 *获取Adobe ID* 证书门户中的链接：

   <!--<a id="fig_mst_gtj_wv"></a>-->

   ![](assets/cert_portal_sign-in-page-web.png)

1. 在Adobe证书门户上，请求 *试用版* 证书。

   对于多DRM试用版，单一试用版证书将涵盖内容保护的所有方面：包装、许可和运输。 您需要提供您自己的 [CSR](../../../digital-rights-management/certificate-enrollment-guide/request-certs/gen-cert-signing-req.md) 要请求证书，请执行以下操作：
   <!--<a id="fig_op1_xwj_wv"></a>-->

   ![](assets/cert_portal_trial_request-web.png)

   Adobe将向您发送一封电子邮件，指明是接受还是拒绝您的证书请求。 您可以在 *请求历史记录* 选项卡：
   <!--<a id="fig_gkl_myj_wv"></a>-->

   ![](assets/cert_portal_request_history-web.png)

1. 创建您的ExpressPlay管理员帐户。

   按照提供给您的Adobe链接到ExpressPlay。 这将打开 *创建帐户* 在ExpressPlay上呼叫。 填写所需信息并提交表单。 您将收到一封来自 `operations@expressplay.com` 包含一个有效期为一周的激活链接。 激活后，请设置ExpressPlay服务：
   <!--<a id="fig_cjl_ztk_wv"></a>-->

   ![](assets/expressplay_create_service-web.png)

   创建服务后，将显示您自己的“管理员”页面。 除了一些活动跟踪字段外，您还将看到生产和测试 *客户验证者* （API密钥），以及您的生产和测试服务URL：

   <!--<a id="fig_c5h_xdl_wv"></a>-->

   ![](assets/expressplay_admin_dashboard_2-web.png) ![](assets/expressplay_admin_dashboard-web.png)

1. 如果您使用的是FairPlay，(在Apple开发人员网站上)还需要执行其他步骤来设置ExpressPlay。 请参阅 [为FairPlay启用ExpressPlay服务](../../multi-drm-workflows/p-l-and-p/fairplay-workflow.md#enable-expressplay-service-for-fairplay) 以获取说明。
