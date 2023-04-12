---
title: Adobe Primetime authentication 2.63发行说明
description: Adobe Primetime authentication 2.63发行说明
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---


# Adobe Primetime Authentication 2.63发行说明 {#pt-authn-263-rn}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

本页介绍此版本的新增功能、更改和已知问题：

## 服务器端和Web客户端 {#server-side-web-clients-263}

* [内部版本号](#build-number)
* [新增功能](#new-features)

### 内部版本号 {#build-number-263}

Adobe Primetime身份验证：adobe-pass-**2.63**
发行日期： **09/20/2022 - 09/22/2022**

### 新增功能 {#new-features-263}

#### 改进平台识别机制 {#pf-identification-mech}

* 从此版本开始，我们改进了用于识别设备的机制，并且不再依赖于客户端实施。 这样，在平台级别应用业务规则时，将提供更准确的粒度，并更好地了解ESM报表中的流量值。

* 随后将发布新的ESM版本，新的和经过改进的报告将公布平台相关领域。

* 有关计划更改的更多详细信息，请联系您的TAM。

#### MVPD自退化 {#mvpd-self-degradation}

此功能为MVPD提供了在相应端点的负载过高时，临时绕过其自身的身份验证和授权端点的功能，以满足高流量情况。


#### 在授权调用的标头中添加代理ID {#add-proxied-id}

此功能可在授权调用的标头中添加代理的同步MVPD的ID。 这样，Synacor就可以为每个代理(例如， 按代理MVPD路由到不同域)。


#### TVE功能板 {#tve-dashboard}

在此版本中，我们修复了配置报表中未正确计算MVPD级别设置的authN或authZ TTL的问题。


#### JavaScript SDK 4.6.0 {#js-sdk}

* 删除了 `eval` 函数，从而使SDK符合内容安全策略。
* 修复了当浏览器的本地存储被合作伙伴应用程序明确清除时，身份验证流程无法成功完成的问题。



