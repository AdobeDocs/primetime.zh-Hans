---
title: 术语表
description: 术语表
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 0%

---


# 术语表 {#glossary}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## AccessEnabler {#accessEnabler}

Adobe Primetime身份验证的客户端组件。 Adobe Primetime身份验证为每个受支持的平台提供了一个AccessEnabler库。

## AuthN {#authn}

用作“AuthN Token”或“AuthN Flow”中“authentication”的简写形式。


## AuthN令牌{#authn-token}

验证令牌，在用户通过MVPD成功验证后，由Adobe Primetime验证生成。 根据程序员的集成平台，令牌会存储在用户设备或Adobe Primetime身份验证服务器上。

## AuthZ {#authz}

用作“授权”的简写，如“AuthZ令牌”或“AuthZ流”中的简写。

## AuthZ令牌 {#authz-token}

授权令牌，在授权用户查看受保护内容后由Adobe Primetime身份验证生成。 AuthZ令牌存储在Adobe Primetime身份验证服务器上，用于生成 [短暂的媒体令牌](#short-lived-token).

## 渠道ID（已弃用） {#channel_id}

资源ID的前一个术语。

## 无客户端API {#clientless-api}

一种Adobe Primetime身份验证集成解决方案，它采用Web服务而不是AccessEnabler客户端组件。

## 设备ID {#device-id}

唯一标识设备（如手机、平板电脑等） 在Adobe Primetime身份验证中。 此ID由程序员的应用程序获取/提供。


## 授权流程{#entitlement_flow}

Adobe Primetime身份验证文档中使用的术语，是指在Adobe Primetime身份验证中注册设备/用户、使用MVPD验证用户、为用户授权资源以及注销用户的整个过程。


## GUID {#guid}

请参阅 [用户ID](#user-id).

## IdP {#idp}

识别提供商；与MVPD在Adobe Primetime身份验证集成中的角色上下文中的同义。 （客户必须通过其付费电视提供商的登录页面验证其身份。）

## 媒体令牌验证器 {#media-token-verifier}

Adobe提供的库，由程序员用来验证在授权流程成功完成后由Adobe Primetime身份验证生成的短期媒体令牌。

## MVPD {#mvpd}

多渠道视频节目分发服务；与“付费电视提供商”同义。

## MVPD ID {#mvpd-id}

请参阅 [用户ID](#user-id).

## 合作伙伴ID {#partner-id}

Adobe传递给MVPD的标识符，MVPD使用它来标识代表Adobe Primetime身份验证请求身份验证的用户。 有时，它用于为特定程序员配置其UI，有时在所有程序员中都是相同的，它取决于MVPD的需求。

## 付费电视提供商 {#pay-tv-provider}

与同义 [MVPD](#mvpd).

## 程序员 {#programmer}

与“内容提供商”、“帐户”、“渠道”、“服务提供商”、“品牌”等同义。

## 代理MVPD {#proxy-mvpd}

为其他MVPD提供身份服务的MVPD;直接与Adobe Primetime身份验证集成。

## 代理的MVPD {#proxied-mvpd}

未与AdobeSP直接集成，但通过代理MVPD集成的MVPD。

## 请求者ID {#requestor-id}

唯一标识 [程序员](#programmer) （帐户、品牌、渠道或属性）。 此ID在初始设置帐户期间由程序员和Adobe确定。 在Web上，请求者ID与一组列入白名单的域相关联；任何使用外部域ID的调用都将被拒绝。 程序员还会使用Analytics的请求者ID。 每个程序员通常只有一个请求者ID。 与请求者ID相关的另一个功能是，程序员必须向Adobe提供公共证书，因为setRequestor API调用希望发送加密数据，该数据用于在Adobe Primetime身份验证系统中验证程序员。

## 资源ID {#resource-id}

用于标识 [程序员](#programmer) 到MVPD。 程序员与MVPD之间已达成协议；Adobe Primetime身份验证会将资源ID传递至未更改的ID，因此所有MVPD的ID必须相同。 只要MVPD知道每个ID代表什么，程序员就可以使用多个资源ID。

## 会话GUID {#sessionGUID}

请参阅 [用户ID](#user-id).

## 短暂的媒体令牌 {#short-lived-token}

此令牌是在特定用户的授权流程成功完成后由Adobe Primetime身份验证生成的。 令牌将传递给程序员，程序员使用短期媒体令牌上的Adobe Primetime身份验证令牌验证器来验证授权过程的安全性。

## 智能设备 {#smart-device}

在整个Adobe Primetime身份验证文档中使用的术语，指机顶盒、游戏机和智能电视。 这些设备具有网络功能，但无法呈现网页。

## SP{#sp}

服务提供商；这通常指 *角色* 由Adobe Primetime身份验证播放，代表程序员与 [MVPD](#mvpd).

## 临时通道 {#temp-pass}

允许程序员提供对付费内容的临时免费访问的功能。 在程序员指定的时间段内，访问是按请求者进行的。

## TTL {#ttl}

活下去。 这是令牌有效的指定时长。

## TVE {#tve}

电视无处不在。

## 用户ID {#user-id}

唯一标识程序员应用程序的用户，但是从MVPD组织。 可在不同表单中用于不同用例。 请参阅 [在程序员概述中了解用户ID](/help/authentication/programmer-overview.md#user-ids).

## 允许列表 {#whitelist}

为与Adobe Primetime身份验证通信而指定为合法的域的列表。

## XSTS令牌 {#xsts-token}

由Microsoft颁发的用于Xbox控制台应用程序开发的安全令牌，用于Xbox/Adobe Primetime身份验证集成。
