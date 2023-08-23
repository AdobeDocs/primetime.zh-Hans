---
title: 在Primetime身份验证量度中使用无客户端deviceType参数的好处
description: 在Primetime身份验证量度中使用无客户端deviceType参数的好处
exl-id: a5004887-d5fa-468e-971b-10806519175b
source-git-commit: 84a16ce775a0aab96ad954997c008b5265e69283
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%

---

# 在Primetime身份验证量度中使用无客户端deviceType参数的好处 {#benefits-of-using-the-clientless-devicetype-parameter-in-primetime-authentication-metrics}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权使用。

</br>

## 上下文

虽然可选，但参数 `deviceType` 来自无客户端API（如果存在）的Primetime身份验证量度用于通过以下方式公开 [授权服务监控](/help/authentication/entitlement-service-monitoring-overview.md).

考虑到 `deviceType` 参数及其 **优点** 在Primetime身份验证量度最初没有明确说明时，本技术说明的范围是添加有关这些量度的更多信息。

## 说明

此 `deviceType` 自第一个版本以来，无客户端API中存在参数，但在较新的版本中添加了它对Primetime身份验证量度的影响。



>[!IMPORTANT]
>
>如果参数 `deviceType` 已正确设置，则它具有以下特征 **收益** 在授权服务监控中：它提供的量度包括 [按设备类型细分](/help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) 使用无客户端应用程序时，以便可以对Roku、AppleTV、Xbox等执行不同类型的分析。


有关授权服务监控API的更多信息，请参阅 [深入分析树，](/help/authentication/entitlement-service-monitoring-api.md#drill-down_tree) 它说明了 [维度](/help/authentication/entitlement-service-monitoring-overview.md#esm_dimensions) （资源）在ESM 2.0中提供。

>[!NOTE]
>
>此技术说明的内容也已添加到 [无客户端API](#clientless_device_type).




## 实现

为了从Primetime身份验证指标中充分受益，有两种类型 [无客户端API](#web_srvs_summary) 当前正在使用，需要拥有正确的 `deviceType` 设置：

1. API具有 `regcode` 作为必需参数，和将使用 `deviceType` 创建时设置的参数 `regcode`，通过以下API调用：
   - [\&lt;reggie _fqdn=&quot;&quot;>/reggie/v1/{requestorId}/regcode](#reg_serv)

1. 具有的API `deviceType` 作为可选参数：
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/checkauthn](#check_authn_token)
   - [&lt;span class=&quot;s1&quot;>](#retrieve_authn_token)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/authorize](#init_authz)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/tokens/authz](#retrieve_authz_token)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/tokens/media](#short_media)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/mediatoken](#short_media)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/preauthorize](#PreAuthZ_Resources)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/logout](#init_logout)

我们建议使用 `deviceType` 参数，并为所有API传递正确的无客户端设备类型。
