---
title: 基于家庭的随时随地电视认证
description: 基于家庭的随时随地电视认证
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1676'
ht-degree: 0%

---


# 基于家庭的随时随地电视认证

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## 什么是基于家庭的身份验证？ {#whatis-home-based-authn}

基于家庭的身份验证(HBA)是一项随时随地电视功能，它使付费电视订阅者在家时无需输入MVPD凭据即可在线查看电视内容，从而显着改善了身份验证流程的用户体验。

开放认证技术委员会(OATC)基于家庭的认证定义：“家庭内自动认证是指MVPD/OVD利用家庭网络的特征（或家庭网络上的设备之间自动访问的标识符）来认证哪个用户帐户与该家庭网络相关联，以便用户在建立用于访问TVE保护内容的TVE会话时不需要手动输入凭据的过程。”



有关HBA和行业标准的详细信息，请阅读 [OATC用例和要求](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/files/Defining%20TVE%20Home-Based%20Authentication%20(HBA)%20%20Use%20Cases%20and%20Requirements%20Recommended%20Practice%20Version%201_0%20FINAL%20DRAFT%20FOR%20BOARD%20APPROVAL.pdf){target=_blank} 文档和 **HBA的OATC用户体验指南**.

>[!NOTE]
>
>某些HBA流是Premium Workflow包的一部分。 如果对使用此功能感兴趣，请联系您的Primetime销售代表。

## 为什么HBA对您很重要 {#why-hba}

HBA很重要，因为它实际上消除了家中已订购电缆的查看器的登录障碍。 此外，基于家庭的身份验证可以显着提高观众的参与度，并为您的TV Everywhere内容提供更好的用户体验。

目前，几乎一半的登录尝试都未成功。

在HBA被前5个MVPD之一激活后，其身份验证转换率 **增加了40%** （从45%到63%）

![](assets/authn-conv-pre-post.png)

此外，您还可以在下面查看与不同MVPD集成的渠道的登录转化率：为HBA启用HBA的和没有HBA的。 具有HBA的用户的转化率比没有HBA的用户高得多。

![](assets/hba-vs-non-hba.png)

在为与此MVPD集成的大多数频道启用HBA六个月后，我们注意到独特用户增加了82%（通过此MVPD访问随时随地电视频道的用户数几乎翻了一番）。

2w3相反，如下图所示，其他未启用HBA的MVPD在过去6个月中的独特用户数量仅增加了26%。

![](assets/unique-visitors-incr.png)

根据我们在启用HBA前6个月和6个月后收集的数据，我们发现查看者对已启用HBA的渠道的参与度显着提高。 实际上，已启用HBA的MVPD用户通常比未启用HBA的MVPD用户观看内容的次数平均多30%。

![](assets/user-engagement-increase.png)

## Primetime身份验证HBA支持 {#auth-hba-support}

本节介绍Primetime身份验证提供的HBA支持、Primetime身份验证平台在HBA流中的行为，并提供有用于实施HBA的技术详细信息。

支持HBA的Primetime身份验证功能

* 能够为HBA与非HBA身份验证设置不同的身份验证TTL（还需要MVPD支持）
* 在身份验证过期时能够自动选择MVPD（跳过MVPD选取器）。 当HBA TTL较小时，这特别有用。
* 能够在验证是否为HBA时向程序员公开（还需要MVPD支持）

### Primetime身份验证平台上的HBA用户体验 {#hba-user-exp}

下表提供了在启用HBA和未启用HBA时支持平台的用户体验的信息：

| 用户流量 — 平台类型 | swf、iOS、Android |
|---|---|
| 启用HBA | 当用户在家时，他们将自动进行身份验证。 在HBA AuthN令牌过期后，用户将自动重新进行身份验证。 |
| 没有HBA | 用户需要选择其MVPD并输入其凭据，即使他们在家。在AuthN令牌过期后，用户必须再次输入其凭据。 |

| 用户流量 — 平台类型 | js， Windows（本机） |
|---|---|
| 启用HBA | 当用户在家时，他们将自动进行身份验证。 在HBA AuthN令牌过期后，用户必须从选取器中重新选择其MVPD，并自动进行身份验证。 |
| 没有HBA | 用户需要选择其MVPD并输入其凭据，即使他们在家。 在AuthN令牌过期后，用户必须再次输入其凭据。 |

| 用户流量 — 平台类型 | 无客户端REST API（第二个屏幕身份验证） |
|---|---|
| 启用HBA | 当用户在家，并且使用无客户端REST API应用程序时，在输入注册代码并选择其MVPD后，会在第二个屏幕设备上自动对其进行身份验证。 在HBA AuthN令牌过期后，用户将自动进行重新身份验证（在第二个屏幕设备上）。 |
| 没有HBA | 用户需要选择其MVPD并输入其凭据，即使他们在家。 在AuthN令牌过期后，用户必须再次输入其凭据。 |

### 实施HBA的技术详细信息 {#tech-details-hba}

#### OAuth 2.0协议 {#oauth-2-protocol}

在与OAuth 2.0身份验证协议集成的MVPD的HBA流中，MVPD会发出刷新令牌，并Adobe会发出HBA身份验证令牌：

* 刷新令牌的TTL由MVPD的业务要求决定。
* HBA身份验证令牌TTL **必须小于或等于** 刷新令牌TTL。


*OAuth 2.0协议的HBA身份验证流程描述*


| 用户操作 | 系统操作 |
|---|---|
| 用户导航到程序员的网站。 尝试播放视频时，会显示MVPD选取器。 用户选择其MVPD并单击登录。 | 进行背景检查。 MVPD应用其规则集进行用户检测(例如，将用户的IP地址映射到分发商配置的调制解调器或宽带连接的机顶盒的MAC地址)。 |
| 屏幕会显示，该屏幕会持续大约3秒。 可以显示插播式广告页面，通知用户正在使用其MVPD帐户自动登录。 | <ol><li>安装在程序员端的AccessEnabler向Adobe Primetime身份验证端点发送身份验证请求（作为HTTP请求）。</li><li>Primetime身份验证端点将请求重定向到MVPD身份验证端点。 <br />**注意：** 请求包含 `hba_flag` 参数（尝试HBA = true），表示MVPD应尝试HBA身份验证。</li><li>MVPD身份验证端点向Adobe Primetime身份验证端点发送授权代码。</li><li>Adobe Primetime身份验证使用授权代码从MVPD令牌端点请求刷新令牌和访问令牌。</li><li>MVPD发送验证决策，并且 `hba_status` (true/false)参数 `id_token`.</li><li>将发送对MVPD用户配置文件端点的调用，以公开 [用户元数据中的hba_status键](/help/authentication/user-metadata-feature.md#obtaining).</li><li>MVPD将刷新令牌TTL设置为MVPD同意的值，Adobe将AuthN令牌TTL设置为小于或等于刷新令牌值的值。</li></ol> |
| 用户已通过身份验证，现在可以浏览授权的“TV Everywhere”内容。 | 身份验证令牌被传递到现在可以成功浏览程序员网站的用户。 |

#### SAML协议 {#saml-protocol}

SAML身份验证协议的HBA身份验证流程描述

| 用户操作 | 系统操作 |
|---|---|
| 用户导航到程序员的网站。 尝试播放视频时，会显示MVPD选取器。 用户选择其MVPD并单击登录。 | 进行背景检查。 MVPD应用其规则集进行用户检测(例如，将用户的IP地址映射到分发商配置的调制解调器或宽带连接的机顶盒的MAC地址)。 |
| 屏幕会显示，该屏幕会持续大约3秒。 可以显示插播式广告页面，通知用户正在使用其MVPD帐户自动登录。 | <ol><li>安装在程序员端的AccessEnabler向Adobe Primetime身份验证端点发送身份验证请求（作为HTTP请求）。</li><li>Primetime身份验证端点将请求重定向到MVPD身份验证端点。</li><li>MVPD应以应包含HBA标志的SAML响应的形式发送身份验证决策：hba_status(true/false)。</li><li>将发送对MVPD用户配置文件端点的调用，以公开 [用户元数据中的hba_status键](/help/authentication/user-metadata-feature.md#obtaining).</li></ol> |
| 用户已通过身份验证，现在可以浏览授权的“TV Everywhere”内容。 | 身份验证令牌被传递到现在可以成功浏览程序员网站的用户。 |


## 如何激活HBA {#how-to-activate-hba}

* **OAuth协议：**
   * 要启用HBA，请参阅 [Primetime TVE Dashboard用户指南](/help/authentication/tve-dashboard-user-guide.md)
* **SAML协议：** 基于家庭的身份验证在MVPD端激活。 程序员或Adobe无需执行任何操作。
有关支持基于主页的身份验证的MVPD的更多信息，请参阅 [MVPD的HBA状态](/help/authentication/hba-status-mvpds.md).

## 常见问题解答 {#faqs}


**问题：** 为何使用SAML和OAuth2协议分离基于主页的身份验证？

**答案：** HBA流对于两种协议是不同的。 从程序员的角度来看，无需采取操作来确保为SAML MVPD启用HBA，而对于OAuth2 MVPD，HBA可以在Primetime TVE仪表板中打开或关闭。



**问题：** 用户是否需要在启用HBA时首次进行身份验证时填写用户名和密码？

**答案：** 不需要，不需要用户名和密码。



**问题：** 如何实施家长监控？

**答案1:** Adobe可以禁用HBA以与需要家长控制批准的渠道进行集成。

**答案2:** Adobe正在对UX文档与OATC合作，该文档建议如何使用家长控制来设置HBA体验。



**问题：** 支持HBA的提供程序是否在HBA的TTL窗口较短，然后它们是否进行常规身份验证？

**答案：** TTL设置是可配置的。 我们建议为HBA身份验证令牌设置较短的TTL，以防止错误处理。


## 有用信息 {#useful-info}

* [即时访问(HBA)Recommendations](http://www.ctamtve.com/instantaccess){target=_blank}  — 由CTAM提供
* [在程序员应用程序上实现HBA的示例](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/files/HBA_Flow_Sample.pdf?dc=201604222139-1346){target=_blank}  — 按Adobe
   <!--* [Home Based Authentication User Experience Guidelines for TV Everywhere](http://oatc.us/Standards/DownloadRecommendedPractices.aspx){target=_blank} - by OATC-->
* [基于家庭的身份验证用例和要求](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/files/Defining%20TVE%20Home-Based%20Authentication%20(HBA)%20%20Use%20Cases%20and%20Requirements%20Recommended%20Practice%20Version%201_0%20FINAL%20DRAFT%20FOR%20BOARD%20APPROVAL.pdf){target=_blank} 由OATC提供
* [基于家庭的身份验证信息图](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/files/AdobeNewsletterHBA.pdf?dc=201604260953-2640){target=_blank}  — 按Adobe
* [使用OAuth 2.0协议进行身份验证](/help/authentication/authn-oauth2-protocol.md)
* [使用SAML MVPD进行身份验证](/help/authentication/authn-usecase.md)
* [Primetime TVE Dashboard用户指南](/help/authentication/tve-dashboard-user-guide.md)
* [hba_status用户元数据](/help/authentication/user-metadata-feature.md#obtaining)



