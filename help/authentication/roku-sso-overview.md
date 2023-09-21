---
title: Roku SSO概述
description: 关于Roku SSO
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# Roku SSO概述 {#overview}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权使用。

## 介绍 {#roku-sso-intro}

本文档介绍了在Roku设备上利用单点登录功能所需的信息。 Adobe Primetime身份验证可与Roku协作以改善登录用户体验，并为电视订阅者实现跨TV Everywhere应用程序的单点登录。

该解决方案基于Adobe Primetime身份验证的无客户端REST API，因此大多数程序员无需更新其应用程序即可从单点登录中获益。

## 启用Roku SSO {#enable-roku-sso}

默认情况下，Roku SSO处于启用状态，除非禁用了SSO的程序员或MVPD请求。

每个程序员都可以在Roku平台上启用/禁用SSO以进行特定集成。

### 程序员应该怎么做才能使Roku SSO正常工作 {#make-roku-sso-work}

对于在客户端设备上实施REST API的程序员应用程序，Roku SSO将无任何更改地工作。 Roku OS将在任何请求中添加两个HTTP标头到Adobe Primetime身份验证端点。

对于为REST API实施服务器到服务器解决方案的程序员应用程序，程序员应联系Roku团队并请求进行配置，以便在所有API流中将这两个标头发送到其域。

使用Roku提供的订阅者ID，而不是应用程序传递的任何设备ID，以确保跨应用程序（和跨设备）SSO。

有关所需标头格式的特定详细信息，请联系您的Adobe代表。

### 可能的问题 {#possible-issues}

程序员应检查其当前基于Adobe无客户端REST API的实施是否不会妨碍Roku的平台 — SSO。 请参阅下面的列表，其中列出了可能的问题以及应如何解决这些问题。

| 问题 | 可能的原因 | 可能的解决方案 |
|-|-|-|
| 未向Adobe发送Roku SSO标头 | 在调用Adobe Primetime身份验证域时使用HTTP而不是HTTPS | 使用HTTPS |
| SSO令牌未显示/未更新MVPD徽标 | UI依赖于本地存储 | 应用程序应在检查身份验证后更新UI（和本地存储，如果需要） |
| 注销（无AuthZ触发） | 应用程序设计 | 应更新应用程序，以免在后台执行注销 |

## 常见问题解答 {#faq}

* **SSO如何工作？**

  SSO将在与同一Roku用户关联的所有Roku设备上运行所有由Adobe Primetime身份验证提供支持的程序员应用程序。
并非所有MVPD都允许Roku SSO。

* **身份验证TTL是否会有任何更改？**

  第一个有效的身份验证令牌将用于执行SSO，在这种情况下，所有其他将通过SSO进行身份验证的应用程序将使用相同的TTL，直到它过期。 因此，当从一个应用程序导航到另一个应用程序时，第二个应用程序将共享验证第一个应用程序的TTL。

* **其他Adobe功能会像以前一样工作吗？**

  所有Primetime身份验证功能都将像以前一样工作。

* **是否存在一个程序员选择加入/选择退出流程受益于Roku平台上的SSO？**

  这将是AdobeTVE仪表板中的配置更改。 每个程序员都可以在Roku平台上启用/禁用SSO以进行特定集成。
