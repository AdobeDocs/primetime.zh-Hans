---
title: 程序员kickstart指南
description: 程序员kickstart指南
exl-id: 0aecdb81-9b97-4475-b0b0-654d916b2374
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 0%

---

# 程序员kickstart指南 {#programmer-kickstart-guide}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权的使用。

## 介绍 {#prog-kickstart-guide-intro}

欢迎使用Adobe Primetime身份验证随时随地访问电视。 我们期待着与您合作。

>[!NOTE]
>
>这是面向程序员（内容提供商）的Kickstart指南。 如果您使用多通道视频节目分发商(MVPD)，请务必查看 [MVPD快速入门指南](/help/authentication/mvpd-kickstart-guide.md).


Adobe Primetime身份验证联系人：

* 支持 — 对于所有问题、事件或功能请求， `tve-support@adobe.com`
* 到项目启动时，会将支持联系人分配给您的项目。

以下信息概述了一些重要的第一步，以便我们开始一个扎实而有效的开始。 我们的目标是提供有关我们将如何与合作伙伴协作以实现集成的解释和期望。 请注意下面每个项目的“您将提供”/“Adobe将提供”部分。 在我们完成项目时，这些内容通过核对清单或指南列出。

本文档假定程序员已注册与选定的MVPD合作伙伴合作。

## 发布计划 {#release-schedule}

我们规划了Adobesprint开发周期，以便您能够查看排程发布的时间以及如何通过我们的开发系统推广每个版本。

在每个冲刺完成后，它可用于QE，或查看UAT服务器上的新实施。

大约每6周会向Adobe资格预审服务器发布一次。 （这是我们在执行最终定量宽松的同时保存所提议的下一个版本的服务器。 ） 这些内部版本将包含自上次放置以来在冲刺中完成的所有工作。 目前提供为期两周的QE窗口，供合作伙伴测试此版本。

假定在前两个星期的测试时段中没有出现任何严重问题，则该版本将提升至实时生产。 这意味着该集成将在Adobe发布环境中可用，但合作伙伴会在公开发布版本时进行选择。

<!--For the latest release schedule information, see the Release Calendar.-->

## 支持文档 {#supp-doc}

Adobe将提供：

* 部署指南： **`https://tve.zendesk.com/entries/498741-tve-deployment-guide`**
* 访问我们的Zendesk客户支持系统。 您还可以在这里找到有关某些流程的示例、信息和视频教程。 要在Zendesk上访问此文档以及发布在该文档上的其他文档，您必须在 `https://tve.zendesk.com/home`. 您可以注册的用户数量没有限制。  您可以查看和共享任何已归档票证的评论。 所有支持问题都应发送至 `tve-support@adobe.com`.
* [程序员集成指南](/help/authentication/programmer-integration-guide-overview.md)
* 媒体令牌验证器库： `https://tve.zendesk.com/entries/471323-media-token-validator-library`.

## 测试环境设置 {#test-env-setup}

Adobe将首先为您设置Adobe测试站点，其中Adobe充当MVPD用于测试。 然后，您的团队可以设置一个调用AdobeAPI的测试网站。 使用默认的MVPD选择器，并选择“Adobe”作为idP。

您将提供：

1. 请求者ID。 这是一个字符串，它将唯一标识向Adobe Primetime身份验证发出请求的网站或应用程序的品牌。 字符串本身是任意的，但需要在Adobe和程序员之间达成一致
1. 渠道信息。 这是一组字符串，用于标识请求者ID所请求的内容渠道。 在许多情况下，渠道和请求者ID是相同的。 但是，您可能拥有同一ID可以请求的多个内容渠道。 频道名称字符串应该与有线电视频道相对应。 某些MVPD将通过AuthN和/或AuthZ协议验证此值。
1. 域名（允许用于该请求者ID）。 这将是一个实际域名列表，Adobe将列出这些域名以接受请求者ID。 这可以确保只有您批准的域才有权使用您的元数据访问Adobe Primetime身份验证。 注意：对于测试/暂存，对生产有效的域名可能不同，应该提供并标识这两个域名。

Adobe将设置帐户，Adobe将提供：

* 用于访问测试站点的登录名和密码

## 使用MVPD设置 {#setup-mvpd}

本节介绍从Adobe测试站点迁移以使用MVPD时需要执行的操作。

您将提供（通过MVPD）：

* **两组凭据**：
   * AuthN + AuthZ ：经过身份验证和授权的用户的登录/密码
   * AuthN + Non-AuthZ ：已验证但未授权的用户的登录/密码
* **资源ID**. 这是一个特定的内容标识符，将通过AuthZ协议通过MVPD进行验证。 这可以在渠道、节目、集或资产级别；它应与您的MVPD商定。

Adobe Primetime身份验证支持基于MRSS的元数据架构，这意味着资源ID可以根据需要具体化，并且可以包含特定MVPD特有的标识符。

**新的MVPD集成**：请务必记住，您选择的MVPD在完成任何集成时都起着不可或缺的作用。 Adobe需要根据每个MVPD的规范为其编写代码。 在这些步骤完成之前，您将无法从对话框中选择该MVPD，也无法完成产品测试。 Adobe需要提前安排此工作，以便与下一个可用冲刺相匹配。 （有关当前计划信息，请参阅发行日历。）

**现有MVPD集成**：如果您选择的MVPD已使用Adobe进行设置，则连接步骤应简单得多（更快），并且通常可以通过配置更改实现连接。

>[!NOTE]
>
>MVPD仍需要启用程序员，并签署任何相关的商业交易。

**带MVPD的QE**：所有集成都将涉及联合QE，并且由于最终用户最终是MVPD的客户，因此许多人在推送“实时”应用程序之前设置了测试周期。 由于这涉及MVPD资源的调度，因此这是一个潜在的延迟区域。

<!--
>[RELATEDINFORMATION]
>[MVPD Kickstart Guide](help\authentication\mvpd-kickstart-guide.md)
-->
