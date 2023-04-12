---
title: MVPD直接集成计划
description: MVPD直接集成计划
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 0%

---


# MVPD启动指南：MVPD直接集成计划 {#mvpd-dir-int-plan}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## 简介 {#mvpd-kickstart-intro}

欢迎使用Adobe Primetime TV Everywhere认证。  我们期待着与你合作。

>[!NOTE]
>
>这是多渠道视频编程分发商(MVPD)的Kickstart指南。 如果您是程序员（内容提供商），请参阅 [程序员Kickstart指南](/help/authentication/programmer-kickstart-guide.md).

Zendesk上的Primetime身份验证票证系统始终提供支持。 您也可以在此处找到适用于我们流程的示例、文档和视频教程。 为了使用 [曾代克](https://adobeprimetime.zendesk.com/)，则必须在https://tve.zendesk.com/home注册并创建帐户。 您可以注册的用户数量以及能够查看或发布对已归档票证的评论的用户数量没有限制。 所有支持问题均应解决：adobe的tve-support

**团队联系人**:

**支持**  — 对于所有问题、事件或功能请求 **tve-support@adobe.com**.

## 1.启动会议 {#kickoff-meetings}

这些会议的范围是Adobe与MVPD之间开始技术讨论。 在此过程中，需要双方共享文档。 作为后续操作，Adobe需要在我们的票证系统(https://tve.zendesk.com/)中开具一个票证，以跟踪集成的状态。

## 2.功能 {#features}

Adobe将设置每周状态调用，以讨论和跟踪集成的整体计划、步骤、时间轴和实施详细信息。 在此阶段，Adobe会审核MVPD的规范。 其结果应该是一个规范页面，该页面详细列出了MVPD所需的所有功能。 MVPD将发送规范文档，详细说明MVPD的身份验证/授权实施。

要澄清的项目，请参阅 [MVPD集成功能](/help/authentication/mvpd-integr-features.md).

此时需要详细描述以下几个设置：

* **MVPD的徽标URL**  — 这是具有以下维度的文件：112 x 33像素。 当用户单击“登录”按钮以选择付费电视提供商时，程序员会在其网站上显示徽标。
* **TTL（存留期）值** - TTL通常由MVPD在身份验证/授权过程中设置。 但是，Adobe可以覆盖这些TTL值，并根据程序员和MVPD所同意的内容提供不同的值。
* **显示名称**  — 当用户单击“登录”按钮以选择付费电视提供商时，节目制作人员会在其网站上显示该内容。
* **测试凭据**  — 两个配置文件（暂存和生产）都应具有测试凭据列表。

>[!IMPORTANT]
>
>每次用户启动授权流时，他都会与单个不透明的唯一用户ID关联。  用户ID用于标识程序员应用程序的用户，但源自MVPD。

>[!CAUTION]
>
>每个MVPD的重要注意事项：用户ID不应包含任何PII（个人身份信息）、可自行或与其他信息一起使用来识别、联系或查找用户的信息。

## 2.元数据交换 {#metadata-ex}

双方需要交换所有涉及的环境（生产、暂存等）的元数据。

* **Adobe**
   * 对于暂存环境Adobe的SP元数据，可从以下位置进行检索： [身份验证暂存sp元数据](https://sp.auth-staging.adobe.com/sp/metadata)
   * 对于生产环境Adobe的SP元数据，可从以下位置进行检索： [身份验证生产sp元数据](https://sp.auth.adobe.com/sp/metadata)

* **MVPD**
   * 添加元数据（暂存/生产）。

## 4.允许IP列表 {#allow-ip-list}

以下IP应在MVPD的防火墙中列入白名单。 请联系Adobe以获取IP列表。

* Primetime身份验证要求在端口80和443上打开防火墙，以允许访问受限资源。

* MVPD需要为身份验证和授权服务器添加IP地址列表（如果是）。

## 5.发展 {#deve}

开发阶段的持续时间将在审查规格后确定，并考虑双方签署的项目。 Adobe需要为授权部分编写自定义代码。

>[!NOTE]
>
>请注意，将按资源执行授权。 授权事务通常使用从程序员站点传递的ID字符串来执行，该ID字符串表示用户请求授权的渠道。 此资源ID是在程序员和MVPD之间建立的，可以根据需要进行粒度分析。

## 6.Adobe环境 {#adobe-env}

Adobe为开发过程的不同阶段提供了不同的环境：

* **资格预审** （准确前）：PRE-QUAL环境包含下一个发行候选项。 Adobe在将集成升级到“发布”环境之前，最初会在此环境中集成新合作伙伴。 合作伙伴有两周时间在PRE-QUAL环境上进行测试，并且必须明确请求对PRE-QUAL配置进行任何更改(请联系您的Adobe代表以了解有关更改请求流程的详细信息)。 错误修复会触发此环境中的新部署。
* **版本** （版本）：Adobe当前的生产内部版本将部署到此处的实时环境。

有关如何使用Adobe环境的更多信息，请参阅 [了解Adobe环境](/help/authentication/understanding-the-adobe-environments.md)

## 7.暂存部署 {#stag-env}

根据从MVPD收到的元数据，Adobe将在Primetime身份验证系统中创建并配置新的MVPD。 这将部署在Adobe的前期暂存环境中，并将配置我们的测试程序员(TestDistributors)。

MVPD需要在其QA/暂存/测试环境中执行相同的部署。

## 8.测试和故障诊断 {#tes-troubleshoot}

在此阶段，Adobe和MVPD测试并排除集成故障。 为帮助测试集成，Primetime身份验证团队可以使用Adobe的API测试网站。 要了解有关使用Adobe的API测试网站的更多信息，请参阅 [使用AdobeAPI测试站点测试身份验证和授权流](/help/authentication/test-authn-authz-flows-using-adobes-api-test-site.md).

成功完成测试和疑难解答后，将在Adobe的版本测试环境中启用该集成。 此时，Adobe可以将MVPD与实际程序员集成。

## 9.生产部署 {#prod-dep}

* MVPD需要先在生产配置文件中部署，才能测试连接。

* Adobe在预先生产中部署。

* 现在，所有各方都可以在生产配置文件中进行测试。

* 如果此时一切正常，Adobe可以将集成移动到版本生产环境（“实时”），该环境对所有用户都可用。

## 10.升级程序 {#esc-proc}

集成投入生产后，提供最佳客户体验就变得至关重要。 为确保在出现服务器关闭问题时获得最佳响应，MVPD必须提供上报过程文档，以便提请Adobe注意的问题。

而Adobe则会向MVPD提供最新的Primetime身份验证升级过程。


<!--- [!RELATEDINFORMATION]
>
>* [Programmer Kickstart Guide](/help/authentication/programmer-kickstart-guide.md)
>* [MVPD Integration Guide](/help/authentication/mvpd-integr-features.md)
-->
