---
title: Amazon fireTV SSO — 程序员启动指南
description: Amazon fireTV SSO — 程序员启动指南
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 0%

---


# Amazon fireTV SSO — 程序员启动指南 {#amazon-firetv-sso---programmer-kick-off-guide}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

</br>

## 简介 {#intro}

本文档介绍了集成新 **Adobe Primetime身份验证的fireTV SDK** 在fireTV应用程序中。 此新SDK利用了Amazon fireTV平台上的操作系统级集成，从而提供 **单点登录** 支持。 要从单点登录中受益，您需要从您的一方进行一些工作，以便将您的应用程序从无客户端API迁移到新的fireTV SDK。 身份验证流中有一些更改，详见下文。

## 高级架构和操作系统级集成 {#high}

为了在Amazon fireTV平台上实现随时随地电视应用程序之间的单点登录并改善该平台上的整体体验，我们决定在fireTV操作系统级别集成我们的核心SDK。 程序员需要根据Adobe提供的存根库进行编译。 实际功能将由Amazon fireTV OS中存在的Adobe库提供。

在Amazon提供fireTV模拟器以在操作系统级别整合我们的库之前，开发只能使用真正的fireTV设备。

## 优点 {#bene}

* 在Amazon fireTV平台上所有Adobe供电的TV Everywhere应用程序之间进行单点登录所有集成的MVPD。
* 能够从HBA中受益（具有支持的MVPD）。
* 能够使用最新的fireTV SDK，而无需在每次发布新SDK版本时更新您的应用程序。
* 所有TVE应用程序都可以通过共享系统库的使用而获益，因为无需拥有AccessEnabler库的本地副本。 这还可确保所有应用程序都使用相同的SDK版本。
* 单屏幕身份验证 — 无需注册代码和第2屏幕工作流。

## 从基于无客户端API的应用程序迁移到基于fireTV SDK的应用程序 {#migra1}

要从无客户端API迁移到fireTV SDK，您需要删除与无客户端API相关的代码库，并集成新的fireTV SDK。

与基于无客户端API的应用程序相比，随着新的fireTV SDK将身份验证移至第一个屏幕，不再需要第二个屏幕身份验证。

这要求程序员在其应用程序中添加MVPD选取器，以便用户能够在fireTV设备上直接选择其电视提供商。 在选择MVPD后，用户将在fireTV设备上看到MVPD登录页面。

FireTV上描述常规、HBA和SSO情景的用户流的线框可在 [Amazon Fire TV - MVVPD登录用户流](https://xd.adobe.com/view/9058288e-4b67-43a1-9d5b-5f76ede6c51e/).

## 从基于Android SDK的应用程序迁移到基于fireTV SDK的应用程序 {#migra2}

这个新的fireTV SDK与我们现有的Android SDK以及我们当前的文档非常相似 **集成我们的Android SDK** <!--http://tve.helpdocsonline.com/android-technical-overview-->在我们准备好fireTV SDK文档之前，可使用。 如果您已经有使用我们的Android SDK的Android应用程序，则fireTV应用程序中fireTV SDK的集成应该会很简单。

与现有的Android SDK相比，在fireTV SDK上，身份验证过程将更简单，因为管理/呈现MVPD登录页面和检索AuthN令牌的任务将由AccessEnabler库在内部执行。

## 常见问题解答 {#faq}

1. 如何 **单点登录** 工作？

   * SSO将跨所有由Adobe Primetime身份验证提供支持的程序员应用程序工作，这些应用程序在同一Amazon fireTV设备上使用新的fireTV SDK
   * 在无客户端REST API上实施的程序员应用程序和在fireTV SDK上实施的应用程序之间使用单点登录(SSO) **将不受支持**

1. FireTV SSO的MVPD覆盖范围是什么？

   * **所有MVPD** 由Adobe Primetime身份验证集成的SSO将在fireTV SDK上提供技术支持。

1. 除了使用新的SDK之外， **工作流更改** 程序员应该注意吗？

   * 程序员需要为fireTV平台实施MVPD选取器。

1. 身份验证是否有任何更改 **TTL**?

   * 与身份验证TTL有关的行为没有变化。
   * 第一个有效的身份验证令牌将用于执行SSO，在这种情况下，所有将通过SSO进行身份验证的其他应用程序将使用相同的TTL，直到其过期。 因此，当从一个应用程序导航到另一个应用程序时，第二个应用程序将共享第一个经过验证的应用程序的TTL。

1. 如何 **退化API** 工作？

   * 降级API不需要任何更改，用户体验将与Android设备上的体验相同。

1. 如何 **TempPass** 流量会受到影响？

   * TempPass流是单屏幕，其行为与任何其他本机设备相同。

1. 其他Adobe功能是否可以像以前一样工作？

   * 所有Primetime身份验证功能将在Android设备上的fireTV上正常工作。
