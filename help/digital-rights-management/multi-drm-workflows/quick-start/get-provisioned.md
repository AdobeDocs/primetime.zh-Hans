---
description: 要开始使用由ExpressPlay提供支持的Primetime DRM云，您需要在Adobe代表的帮助下设置Adobe证书和ExpressPlay帐户。
title: 配置（帐户等）
exl-id: 2543d997-3495-4545-9395-072c07431aba
source-git-commit: a0917e128862184ce18050792c2ee2ac265050d2
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---

# 配置（帐户等） {#get-provisioned-accounts-etc}

要开始使用由ExpressPlay提供支持的Primetime DRM云，您需要在Adobe代表的帮助下设置Adobe证书和ExpressPlay帐户。

1. 联系您的Adobe代表，并请求Adobe证书和ExpressPlay帐户，以便您使用TVSDK实施多DRM。

   向您的Adobe代表提供您将用作联系人的电子邮件地址。 Adobe，然后为您创建两个帐户：

   * ***证书门户帐户*** -(https://certportal.primetime.adobe.com):的 *Adobe访问/ Primetime DRM证书注册管理团队* 向您提供的地址发送电子邮件。 该电子邮件包含Adobe证书门户的URL，以及指向Adobe证书注册文档的链接(以下是最新文档： [证书注册指南](../../../digital-rights-management/certificate-enrollment-guide/about-certs.md))。

   * ***ExpressPlay帐户*** -Adobe向您发送一封电子邮件，其中包含用于注册ExpressPlay管理员帐户的链接。

1. 使用Adobe ID登录Adobe证书门户(使用您向Adobe代表提供的相同电子邮件地址)。 如果您还没有Adobe ID，则可以按照 *获取Adobe ID* 证书门户中的链接：

   <!--<a id="fig_mst_gtj_wv"></a>-->

   ![](assets/cert_portal_sign-in-page-web.png)

1. 在Adobe证书门户上，请求 *试用版* 证书。

   对于多DRM试用版，单个试用证书将涵盖内容保护的所有方面：包装、许可和运输。 您需要提供自己的 [CSR](../../../digital-rights-management/certificate-enrollment-guide/request-certs/gen-cert-signing-req.md) 请求证书：
   <!--<a id="fig_op1_xwj_wv"></a>-->

   ![](assets/cert_portal_trial_request-web.png)

   Adobe将向您发送电子邮件，指示接受或拒绝您的证书请求。 您可以在 *请求历史记录* 选项卡：
   <!--<a id="fig_gkl_myj_wv"></a>-->

   ![](assets/cert_portal_request_history-web.png)

1. 创建您的ExpressPlay管理员帐户。

   请点击该Adobe提供给您的ExpressPlay链接。 这将打开 *创建帐户* 页面。 填写所需信息并提交表格。 您将收到来自 `operations@expressplay.com` 包含一周内有效的激活链接。 激活后，请设置ExpressPlay服务：
   <!--<a id="fig_cjl_ztk_wv"></a>-->

   ![](assets/expressplay_create_service-web.png)

   创建服务后，您将获得自己的管理员页面。 除了一些活动跟踪字段外，您还会看到生产和测试 *客户身份验证器* （API密钥），以及您的生产和测试服务URL:

   <!--<a id="fig_c5h_xdl_wv"></a>-->

   ![](assets/expressplay_admin_dashboard_2-web.png) ![](assets/expressplay_admin_dashboard-web.png)

1. 如果您使用FairPlay，则还需要执行其他步骤(在Apple开发人员网站上)来设置ExpressPlay。 请参阅 [为FairPlay启用ExpressPlay服务](../../multi-drm-workflows/p-l-and-p/fairplay-workflow.md#enable-expressplay-service-for-fairplay) 中。
