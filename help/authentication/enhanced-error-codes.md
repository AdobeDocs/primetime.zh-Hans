---
title: 增强的错误代码
description: 增强的错误代码
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2356'
ht-degree: 2%

---

# 增强的错误代码 {#enhanced-error-codes}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## 概述 {#overview}

本文档介绍API错误代码的列表以及返回给应用程序的其他错误信息。

要在程序员应用程序中使用增强的错误代码，需要向支持团队发出请求，以便通过配置更改来启用该代码。

## 响应错误处理 {#response-error-handling}

在大多数情况下，Primetime身份验证API在响应正文中包含其他错误信息，以便提供 **有意义的上下文** 以说明发生特定错误的原因和/或自动修正问题的可能解决方案。  *但是，在某些涉及身份验证或注销流的特定情况下，Primetime身份验证服务可能会返回HTML响应或空主体 — 有关更多信息，请查看API文档。*

虽然某些类型的错误可以自动处理（例如，在网络超时时重试授权请求，或在其会话过期时要求用户重新进行身份验证），但其他类型可能需要更改配置或客户关怀团队交互。 对于程序员来说，在此类情况下收集并提供完整的错误信息非常重要。

Primetime身份验证API会返回范围为400-500的HTTP状态代码，以指示失败或错误。 每个HTTP状态代码都会产生某些影响：

- 4xx错误代码表示错误是由客户端生成的，并且客户端需要执行其他工作来修复它（例如，在调用受保护的API或提供任何必需的参数之前获取访问令牌）

- 5xx错误代码表示错误是由服务器生成的，并且服务器需要执行其他工作来修复它。

其他错误信息包含在响应正文的“error”字段中。 




| 名称 | 类型 | 示例 | 描述 |
| --- | --- | --- | --- |
| **错误** | _对象_ | JSON <br>    {<br>        &quot;status&quot; :403,<br>        &quot;code&quot; :&quot;network_connection_failure&quot;,<br>        &quot;message&quot; :“无法联系您的电视提供商服务”，<br>        &quot;helpUrl&quot; :&quot;&quot;,<br>        &quot;trace&quot; :&quot;12f6fef9-d2e0-422b-a9d7-60d799abe353&quot;,<br>        &quot;action&quot; :&quot;retry&quot;<br>    }<br><br>—<br><br>XML<br><br>`<``error``>`<br><br>`<``status``>403</``status``>`<br><br>`<``code``>network_connection_failure</``code``>`<br><br>`<``message``>Unable to contact your TV provider services</``message``>   <``helpUrl``></``helpUrl``>`<br><br>`<``trace``>12f6fef9-d2e0-422b-a9d7-60d799abe353</``trace``>`<br><br>`<``action``>retry</``action``>`<br><br>`</``error``> ` | 尝试完成请求时收集的集合或错误对象。 |

</br>

处理多个项目（预授权API等）的Adobe Primetime API可能会通过使用项目级别的错误信息来指示处理特定项目是否失败，以及处理其他项目是否成功。 在本例中， ***&quot;error&quot;*** 对象位于项目级别，且响应主体可能包含多个 ***&quot;errors&quot;*** 对象 — 请查阅API文档。

</br>

| 部分成功和项目级错误的示例 |
| ---------------------- |
| <pre lang="json">JSON <br>{<br>  &quot;id&quot; :&quot;TestStream1&quot;,<br>  “已授权”：true <br>}, </br>{ </br>  &quot;id&quot; :&quot;TestStream2&quot;, <br>   “已授权”：false， </br>   &quot;error&quot; :{ <br> </br>      &quot;status&quot; :403,<br>      &quot;code&quot; :&quot;network_connection_failure&quot;,<br>      &quot;message&quot; :“无法联系您的电视提供商服务”，<br>      “详细信息”：&quot;&quot;,<br>      &quot;helpUrl&quot; :&quot;&quot;,<br>      &quot;trace&quot; :&quot;8bcb17f9-b172-47d2-86d9-3eb146eba85e&quot;,<br>      &quot;action&quot; :&quot;retry&quot;</br>    }<br> </br>   }<br> ] </br>} </pre> |

</br>

每个错误对象都具有以下参数：

| 名称 | 类型 | 示例 | 受限 | 描述 |
|----|----|----|----|--------------|
| 状态 | *整数* | 403 | ♦ | RFC 7231(https://tools.ietf.org/html/rfc7231#section-6)中记录的响应HTTP状态代码 <br> - 400错误请求 <br> - 400错误请求 <br> - 400错误请求 <br> - 401未授权 <br>  — 禁止403 <br> - 404未找到 <br> - 405不允许的方法 <br> - 409冲突 <br> - 410已不存在 <br> - 412先决条件失败 <br> - 429请求过多 <br> - 500间隔服务器错误 <br> - 503服务不可用 |
| 代码 | *字符串* | network_connection_failure | ♦ | 标准的Primetime身份验证错误代码。 错误代码的完整列表如下所示。 |
| 消息 | *字符串* | 无法联系您的电视提供商服务 |  | 可向最终用户显示的人类可读消息。 |
| 详细信息 | *字符串* | 您的订阅包不包含“实时”渠道 |  | 在某些情况下，MVPD授权端点或程序员通过降级规则提供详细消息。 <br> <br> 请注意，如果未从合作伙伴服务收到自定义消息，则错误字段中可能不存在此字段。 |
| helpUrl | *url* | &quot;&quot; |  | 一个URL，链接到有关发生此错误的原因和可能解决方案的更多信息。 <br> <br>  URI表示绝对URL，不应从错误代码中推断该URI。 根据错误上下文，可以提供不同的URL。 例如，相同bad_request错误代码将为身份验证和授权服务生成不同的url。 |
| trace | *字符串* | 12f6fef9-d2e0-422b-a9d7-60d799abe353 |  | 此响应的唯一标识符，在联系支持人员以识别更复杂情景中的特定问题时可使用。 |
| 操作 | *字符串* | 重试 | ♦ | *建议采取以下操作来纠正这种情况：* </br><br> -none — 遗憾的是，没有预定义操作来修正此问题。 这可能表示公共API调用不当 </br><br>-configuration — 需要通过TVE功能板或通过联系支持人员进行配置更改。 </br><br>-application-registration — 应用程序必须重新注册自身。 </br><br>-authentication — 用户必须进行身份验证或重新进行身份验证。 </br><br>-authorization — 用户必须获得特定资源的授权。 </br><br> — 退化 — 应采用某种形式的退化。 </br><br>-retry — 重试请求可能会解决问题</br><br>-retry-after — 在指定的时间段后重试请求可能会解决此问题。 |

</br>

**注意：**

- ***受限*** 列 *指示相应的字段值是否表示有限集* (例如“”的现有HTTP状态代码&#x200B;*状态*”字段。 以后对此规范的更新可能会向受限列表添加值，但不会删除或更改现有值。 非限制字段通常可以包含任何数据，但可能存在一些限制，以确保大小合理。

- 每个Adobe响应都将包含一个“Adobe请求ID”，用于在整个HTTP服务中标识客户端请求。 “**trace**“字段补充了这一点，它们应该一起报告。 

## HTTP状态代码和错误代码 {#http-status-codes-and-error-codes}

由于对旧sdk和应用程序(例如， *unknown\_application* 生成400个错误请求，而 *未知\_software\_statement* 产生401未授权)。 解决这些不一致问题将在未来的迭代中成为目标。 
 
## 操作和错误代码 {#actions-and-error-codes}

对于大多数错误代码，多个操作都可以作为修复当前问题的路径，甚至可能需要多个操作才能自动修复它们。 我们选择指示错误修复概率最高的错误。 的 **操作** 可以分为三类：

1. 尝试修复请求上下文的上下文（重试，重试后） 
1. 尝试在应用程序中修复用户上下文的应用程序（应用程序注册、身份验证、授权） 
1. 尝试修复应用程序与身份提供程序之间的集成上下文（配置、降级）的

对于第一个类别（重试后重试），只需重试同一请求就足以解决问题。 如果API处理多个项目，应用程序应重复该请求，并仅包含那些具有“重试”或“重试后”操作的项目。 对于“*重试后*&quot;操作， a &quot;<u>Retry-After</u>“标头将指示应用程序在重复请求之前应等待多少秒。

对于第2和第3类，实际操作实施与应用程序功能有很大关系。 例如，“*降解*“可以作为“切换到15分钟的临时传递以允许用户播放内容”实施，也可以作为“自动工具，对与指定MVPD的集成应用AUTHN-ALL或AUTHZ-ALL降级”。 类似于“*身份验证*“ action可在平板电脑上触发被动身份验证（后台身份验证），并在连接的电视上触发第2屏全屏身份验证流程。 因此，我们选择为功能齐全的URL提供架构和所有参数。 

## 错误代码 {#error-codes}

下面的错误表列出了可能的错误代码、关联的消息和可能的操作。

| 操作 | 错误代码 | HTTP状态代码 | 描述 |
|---|---|---|--------------|
| 配置 | *authorization_denied_by_mvpd* | 403 | MVPD在请求对指定资源的授权时返回了“拒绝”决定。 |
|  | *authorization_denied_by_parent_controls* | 403 | 由于指定资源的家长控制设置，MVPD已返回“拒绝”决策。 |
|  | *authorization_denied_by_programmer* | 403 | 程序员应用的降级规则强制对当前用户做出“拒绝”决定。 |
|  | *bad_request* | 400 | API请求无效或格式不正确。 查看API文档以确定请求要求。 |
|  | *个性化服务不可用* | 503 | 由于个性化服务不可用，请求失败。 |
|  | *internal_error* | 500 | 由于内部服务器错误，请求失败。 |
|  | *invalid_client_time* | 400 | 未正确设置客户端计算机Date / Time / Timezone。 这可能会导致身份验证/授权错误。 |
|  | *invalid_custom_scheme* | 400 | 无法识别应用程序注册中使用的指定自定义方案。 请检查TVE仪表板配置，以确定合适的自定义方案值。 |
|  | *invalid_domain* | 400 | 请求者使用的域无效。 特定请求者ID使用的所有域都需要按Adobe列入白名单。 |
|  | *invalid_header* | 400 | 请求失败，因为它包含无效标头。 查看API文档，以确定哪些标头对您的请求有效以及它们的值是否存在任何限制。 |
|  | *invalid_http_method* | 405 | 不支持与请求关联的HTTP方法。 查看API文档，以确定适用于您请求的受支持HTTP方法。 |
|  | *invalid_parameter_value* | 400 | 请求失败，因为它包含无效的参数或参数值。 查看API文档，以确定哪些参数对您的请求有效以及这些参数的值是否存在任何限制。 |
|  | *invalid_resource_value* | 400 | 请求失败，因为使用的资源无效或格式错误。 查看API文档，以确定针对您的请求必须对复杂资源进行编码的方式，以及这些资源的值和/或大小是否存在任何限制。 |
|  | *invalid_registration_code | 404 | 指定的注册代码不再有效或已过期。 |
|  | *invalid_service_configuration* | 500 | 请求因服务配置不正确而失败。 |
|  | *missing_authentication_header* | 400 | 请求失败，因为它不包含特定API所需的身份验证标头。 |
|  | *missing_resource_mapping* | 400 | 指定的资源没有相应的映射。 联系支持人员以修复所需的映射。 |
|  | *preauthorization_denied_by_mvpd* | 403 | MVPD在请求对指定资源的预授权时返回了“拒绝”决定。 |
|  | *preauthorization_denied_by_programmer* | 403 | 程序员应用的降级规则强制对当前用户执行“拒绝”决定。 |
|  | *registration_code_service_unavailable* | 503 | 请求失败，因为注册代码服务不可用。 |
|  | *service_unavailable | 503 | 由于身份验证或授权服务不可用，请求失败。 |
|  | *access_token_unavailable* | 400 | 检索访问令牌时出现意外错误，导致请求失败。 请检查TVE仪表板配置，以查找可用的软件报表和已注册的自定义方案。 |
|  | *unsupported_client_version* | 400 | 此版本的Primetime身份验证SDK过旧，不再受支持。 有关升级到最新版本所需的步骤，请查看API文档。 |
|  | *network_required_ssl* | 403 | 目标合作伙伴服务存在SSL连接问题。 请联系支持团队。 |
|  | *too_many_resources* | 403 | 授权或预授权请求失败，因为查询的资源过多。 请联系支持团队以正确配置授权和预授权限制。 |
|  | *unknown_programmer | 400 | 程序员或服务提供商无法识别。 使用TVE Dashboard注册指定的程序员。 |
|  | *unknown_application* | 400 | 无法识别该应用程序。 使用TVE仪表板注册指定的应用程序。 |
|  | *unknown_integration* | 400 | 指定的程序员和身份提供者之间不存在集成。 使用TVE功能板创建所需的集成。 |
|  | *unknown_software_statement* | 401 | 无法识别与访问令牌关联的软件语句。 请联系支持团队以阐明软件声明的状态。 |
| 应用注册 | *access_token_expired* | 401 | 访问令牌已过期。 应用程序应按照API文档中的说明刷新访问令牌。 |
|  | *invalid_access_token_signature* | 401 | 访问令牌签名不再有效。 应用程序应按照API文档中的说明刷新访问令牌。 |
|  | *invalid_client_id* | 401 | 无法识别关联的客户端标识符。 应用程序应遵循API文档中所述的应用程序注册流程。 |
| 身份验证 | *authentication_session_expired* | 410 | 当前身份验证会话已过期。 用户必须使用支持的MVPD进行重新身份验证才能继续。 |
|  | *authentication_session_missing* | 401 | 无法检索与此请求关联的身份验证会话。 用户必须使用支持的MVPD进行重新身份验证才能继续。 |
|  | *authentication_session_unvalidated* | 401 | 身份验证会话被身份提供者失效。 用户必须使用支持的MVPD进行重新身份验证才能继续。 |
|  | *authentication_session_issuer_mismatch | 400 | 授权请求失败，原因是为授权流指示的MVPD与发出身份验证会话的MVPD不同。 用户必须使用所需的MVPD进行重新身份验证才能继续。 |
|  | *authorization_denied_by_hba_policies* | 403 | 由于基于家庭的身份验证策略，MVPD返回了“拒绝”决策。 当前验证是使用基于家庭的验证流程(HBA)获取的，但在请求对指定资源的授权时，设备不再位于家中。 用户必须使用支持的MVPD进行重新身份验证才能继续。 |
|  | *identity_not_recogned_by_mvpd* | 403 | 由于MVPD无法识别用户身份，授权请求失败。 |
| 授权 | *authorization_expired* | 410 | 指定资源的先前授权已过期。 用户必须获得新授权才能继续。 |
|  | *authorization_not_found* | 404 | 未找到指定资源的授权。 用户必须获得新授权才能继续。 |
|  | *device_identifier_mistach* | 403 | 指定的设备标识符与授权设备标识不匹配。 用户必须获得新授权才能继续。 |
| 重试 | **network_connection_failure** | 403 | 与关联的合作伙伴服务发生连接失败。 重试该请求可能会解决此问题。 |
|  | *network_connection_timeout* | 403 | 关联的合作伙伴服务存在连接超时。 重试该请求可能会解决此问题。 |
|  | *network_received_error* | 403 | 从关联的合作伙伴服务检索响应时出现读取错误。 重试该请求可能会解决此问题。 |
|  | *maximum_execution_time_exceeded* | 403 | 请求未在允许的最长时间内完成。 重试该请求可能会解决此问题。 |
| 重试后 | *too_many_requests* | 429 | 在给定间隔内发送的请求过多。 在建议的时间段后，应用程序可以重试请求。 |
|  | *user_rate_limit_exceeded* | 429 | 特定用户在给定间隔内发出的请求过多。 在建议的时间段后，应用程序可以重试请求。 |

