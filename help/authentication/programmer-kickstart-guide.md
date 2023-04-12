---
title: 程序员启动指南
description: 程序员启动指南
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 0%

---


# 程序员启动指南 {#programmer-kickstart-guide}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## 简介 {#prog-kickstart-guide-intro}

欢迎使用Adobe Primetime TV Everywhere认证。 我们期待着与你合作。

>[!NOTE]
>
>这是面向程序员（内容提供商）的Kickstart指南。 如果您使用的是多渠道视频节目分发服务(MVPD)，请务必查看 [MVPD启动指南](/help/authentication/mvpd-kickstart-guide.md).


Adobe Primetime身份验证联系人：

* 支持 — 适用于所有问题、事件或功能请求， `tve-support@adobe.com`
* 在项目启动时，您的项目将分配一个支持联系人。

以下信息概述了一些重要的首要步骤，以便我们能够立即开始，并实现高效的开始。 我们的目标是针对我们如何与合作伙伴合作来实现集成，提供一种解释和期望。 请注意下面每个项目的“您将提供”/“Adobe将提供”部分。 在我们完成项目时，这些内容会通过核对表或指南列出。

本文档假定程序员已注册，可与所选的MVPD合作伙伴合作。

## 发行计划 {#release-schedule}

Adobe冲刺开发周期已经计划完成，以便您查看我们的版本计划时间以及每个版本如何通过我们的开发系统进行推广。

每次冲刺完成后，即可进行QE，或在UAT服务器上查看新实施。

大约每6周向Adobe资格预审服务器发布一次。 （这是我们在执行最终QE时，暂停提议的下一版本的服务器。） 这些内部版本将包含自上次删除后在Sprint中完成的所有工作。 目前，合作伙伴可以使用两周的QE时间来测试此版本。

如果在前两周的测试时间范围内未出现任何关键问题，此版本将被提升为正式生产。 这意味着该集成将在Adobe发布环境中可用，但合作伙伴可以选择何时发布该版本。

<!--For the latest release schedule information, see the Release Calendar.-->

## 支持文档 {#supp-doc}

Adobe将提供：

* 部署指南： **`https://tve.zendesk.com/entries/498741-tve-deployment-guide`**
* 访问我们的Zendesk客户支持系统。 您也可以在此处找到一些流程的示例、信息和视频教程。 若要在Zendesk上访问此文档，以及在其中发布的其他文档，您必须在 `https://tve.zendesk.com/home`. 您可以注册的用户数量没有限制。  您可以查看和共享任何归档票证上的评论。 所有支持问题均应解决 `tve-support@adobe.com`.
* [程序员集成指南](/help/authentication/programmer-integration-guide-overview.md)
* 媒体令牌验证器库： `https://tve.zendesk.com/entries/471323-media-token-validator-library`.

## 测试环境设置 {#test-env-setup}

Adobe将首先设置您的Adobe测试网站，在该网站中，Adobe将充当MVPD以进行测试。 然后，您的团队可以设置一个测试网站，以调用AdobeAPI。 使用默认的MVPD选择器，然后选择“Adobe”作为idP。

您将提供：

1. 请求者ID。 这是一个字符串，用于唯一标识向Adobe Primetime身份验证请求的网站或应用程序的品牌。 字符串本身是任意的，但需要在Adobe与程序员之间达成一致
1. 渠道信息。 这是一组字符串，用于标识请求者ID请求的内容渠道。 在许多情况下，渠道和请求者ID是相同的。 但是，您可能有多个内容渠道，这些渠道可由同一ID请求。 频道名称字符串应与有线电视频道相对应。 某些MVPD将通过AuthN和/或AuthZ协议验证此值。
1. 域名（允许该请求者ID使用）。 这将是实际域名的列表，Adobe将列出这些域名以接受请求者ID。 这可确保只有已批准的域才有权使用您的元数据访问Adobe Primetime身份验证。 注意：对于测试/暂存而言，对于生产有效的域名可能不同，应提供并识别这两个域名。

Adobe将设置帐户，Adobe将提供：

* 访问测试网站的登录名和密码

## 使用MVPD进行设置 {#setup-mvpd}

本节介绍从Adobe测试网站迁移以使用MVPD时需要满足的条件。

您将提供（通过MVPD）：

* **两组凭据**:
   * AuthN + AuthZ :经过身份验证和授权的用户的登录/密码
   * AuthN +非AuthZ :已验证但未授权的用户的登录/密码
* **资源ID**. 这是将通过AuthZ协议通过MVPD验证的特定内容标识符。 这可以是在渠道、节目、剧集或资产级别；应与您的MVPD协议。

Adobe Primetime身份验证支持基于MRSS的元数据架构，这意味着资源ID可以根据需要进行特定的标识，并且可以包含对特定MVPD可能唯一的标识符。

**新的MVPD集成**:请务必记住，您选择的MVPD在完成任何集成过程中起着不可或缺的作用。 Adobe需要根据每个MVPD的规范为其编写代码。 在这些步骤完成之前，您将无法从对话框中选择该MVPD，或完成产品测试。 Adobe需要提前安排这项工作，以适应下一次的冲刺。 （有关当前计划信息，请参阅发行日历。）

**现有MVPD集成**:如果您选择的MVPD已通过Adobe进行设置，则连接步骤应该更简单（更快），并且通常可以通过配置更改来实现连接。

>[!NOTE]
>
>MVPD仍然必须启用程序员，并签署任何相关的业务协议。

**QE与MVPD**:所有集成都将涉及联合QE，由于最终用户最终是MVPD的客户，因此许多集成在推出“正式启用”之前已设置了测试周期。 由于这涉及MVPD资源的调度，因此这是一个潜在的延迟区域。

<!--
>[RELATEDINFORMATION]
>[MVPD Kickstart Guide](help\authentication\mvpd-kickstart-guide.md)
-->

