---
title: 在Primetime身份验证量度中使用无客户端deviceType参数的好处
description: 在Primetime身份验证量度中使用无客户端deviceType参数的好处
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%

---


# 在Primetime身份验证量度中使用无客户端deviceType参数的好处 {#benefits-of-using-the-clientless-devicetype-parameter-in-primetime-authentication-metrics}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

</br>

## 上下文

尽管该参数是可选的，但 `deviceType` （如果存在），则会用在通过公开的Primetime身份验证量度中 [授权服务监控](/help/authentication/entitlement-service-monitoring-overview.md).

考虑到 `deviceType` 参数及其 **好处** 在Primetime身份验证量度最初未说明时，此技术说明的范围是添加有关这些量度的更多信息。

## 说明

的 `deviceType` 参数自第一个版本起便出现在无客户端API中，但在更新版本中添加了它对Primetime身份验证量度的影响。



>[!IMPORTANT]
>
>如果参数 `deviceType` 设置正确，则具有以下内容 **效益** 在授权服务监控中：它提供了 [按设备类型划分](/help/authentication/entitlement-service-monitoring-overview.md#clientless_device_type) 使用无客户端时，以便可以对Roku、AppleTV、Xbox等执行不同类型的分析。


有关授权服务监控API的更多信息，请参阅 [向下钻取树，](/help/authentication/entitlement-service-monitoring-api.md#drill-down_tree) 说明 [维度](/help/authentication/entitlement-service-monitoring-overview.md#esm_dimensions) （资源）可在ESM 2.0中使用。

>[!NOTE]
>
>此技术说明的内容也添加到 [无客户端API](#clientless_device_type).




## 实施

要充分利用Primetime身份验证量度，有2种类型 [无客户端API](#web_srvs_summary) 当前正在使用且需要正确 `deviceType` 设置：

1. 具有 `regcode` 作为必需参数，并将使用 `deviceType` 参数，创建时设置 `regcode`，并使用以下API调用：
   - [\&lt;reggie _fqdn=&quot;&quot;>/reggie/v1/{requestorId}/regcode](#reg_serv)

1. 具有 `deviceType` 作为可选参数：
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/checkauthn](#check_authn_token)
   - [&lt;span class=&quot;s1&quot;>](#retrieve_authn_token)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/authorize](#init_authz)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/tokens/authz](#retrieve_authz_token)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/tokens/media](#short_media)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/mediatoken](#short_media)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/preauthorize](#PreAuthZ_Resources)
   - [\&lt;sp _fqdn=&quot;&quot;>/api/v1/logout](#init_logout)

我们的建议是使用 `deviceType` 参数并为所有API传递正确的无客户端设备类型。


