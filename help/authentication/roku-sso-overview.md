---
title: Roku SSO概述
description: 关于Roku SSO
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---


# Roku SSO概述 {#overview}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## 简介 {#roku-sso-intro}

本文档介绍在Roku设备上利用单点登录功能所需的信息。 Adobe Primetime身份验证与Roku协作，以改善登录用户体验，并为电视订阅者提供跨TV Everywhere应用程序的单点登录。

此解决方案基于Adobe Primetime身份验证的无客户端REST API，因此大多数程序员无需更新其应用程序即可从单点登录中受益。

## 启用Roku SSO {#enable-roku-sso}

默认情况下，Roku SSO处于启用状态，除非程序员或MVPD请求禁用SSO。

每个程序员都可以在Roku平台上启用/禁用单点登录(SSO)，以进行特定集成。

### 程序员应该如何使Roku SSO工作 {#make-roku-sso-work}

对于在客户端设备上实施REST API的程序员应用程序，Roku SSO将可以正常工作，而无需进行任何更改。 Roku OS将在任何请求中向Adobe Primetime身份验证端点添加两个HTTP标头。

对于为REST api实施服务器到服务器解决方案的程序员应用程序，程序员应与Roku团队联系，并请求进行配置，以在所有api流中将这两个标头发送到其域。

Roku提供的订阅者ID，将用来代替应用程序传递的任何设备ID，以确保跨应用程序（和跨设备）SSO。

有关所需标头格式的具体详细信息，请联系您的Adobe代表。

### 可能的问题 {#possible-issues}

程序员应检查其当前基于Adobe无客户端REST API的实施是否不会妨碍Roku的平台SSO。 请参见下面的问题列表，以及应如何解决这些问题。

|问题 |可能的原因 |可能的解决方案 | |-|-|-| |未将Roku SSO标头发送到Adobe|对Adobe Primetime身份验证域调用使用HTTP而不是HTTPS|使用HTTPS| |未显示/未更新SSO令牌的MVPD徽标|UI依赖于本地存储|应用程序应在检查身份验证后更新UI(和本地存储（如果需要）)| |在无AuthZ时触发注销|应用程序设计|应更新应用程序，以免在后台执行注销|

## 常见问题解答 {#faq}

* **单点登录将如何工作？**

   SSO将在与同一Roku用户关联的所有Roku设备上跨所有由Adobe Primetime身份验证提供支持的程序员应用程序工作。
并非所有MVPD都允许使用Roku SSO。

* **验证TTL是否有任何更改？**

   第一个有效的身份验证令牌将用于执行SSO，在这种情况下，所有将通过SSO进行身份验证的其他应用程序将使用相同的TTL，直到其过期。 因此，当从一个应用程序导航到另一个应用程序时，第二个应用程序将共享经验证的第一个应用程序的TTL。

* **其他Adobe功能是否可以像以前一样工作？**

   所有Primetime身份验证功能将像以前一样正常工作。

* **在Roku平台上，是否有程序员选择加入/选择退出流程可从单点登录(SSO)中受益？**

   这将是AdobeTVE功能板中的配置更改。 每个程序员都可以在Roku平台上启用/禁用单点登录(SSO)，以进行特定集成。
