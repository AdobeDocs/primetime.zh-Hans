---
title: Amazon FireOS集成指南
description: Amazon FireOS集成指南
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1433'
ht-degree: 0%

---


# Amazon FireOS集成指南 {#amazon-fireos-integration-cookbook}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

</br>


## 简介 {#intro}

本文档介绍程序员的高级应用程序可以通过由Amazon FireOS AccessEnabler库公开的API来实施的权利工作流程。

Amazon FireOS的Adobe Primetime身份验证授权解决方案最终分为两个域：

- UI域 — 这是实施UI并使用AccessEnabler库提供的服务提供对受限内容的访问的上层应用程序层。
- AccessEnabler域 — 在此域中，授权工作流以以下形式实施：
   - 对Adobe后端服务器进行的网络调用
   - 与身份验证和授权工作流相关的业务逻辑规则
   - 管理各种资源并处理工作流状态（如令牌缓存）

AccessEnabler域的目标是隐藏授权工作流的所有复杂性，并（通过AccessEnabler库）向上层应用程序提供一组简单的授权基元，您可以使用这些基元实施授权工作流：

1. 设置请求者身份
1. 针对特定身份提供者检查并获取身份验证
1. 检查并获取特定资源的授权
1. 注销

AccessEnabler的网络活动在不同线程中进行，因此UI线程从不被阻止。 因此，两个应用程序域之间的双向通信信道必须遵循完全异步模式：

- UI应用层通过AccessEnabler库公开的API调用，将消息发送到AccessEnabler域。
- AccessEnabler通过AccessEnabler协议中包含的回调方法响应UI层，UI层向AccessEnabler库注册该回调方法。

## 权利流 {#entitlement}

1. [先决条件](#prereqs)
1. [启动流程](#startup_flow)
1. [身份验证流程](#authn_flow)
1. [授权流程](#authz_flow)
1. [查看媒体流量](#media_flow)
1. [注销流程](#logout_flow)

 

### A.先决条件 {#prereqs}

1. 创建回调函数：
   - [&#39;setRequestorComplete()&#39;](#$setRequestorComplete)

      - 触发者 `setRequestor()`，则返回成功或失败。     成功表示您可以继续进行授权调用。
   - [displayProviderDialog(mvpds)](#$displayProviderDialog)

      - 触发者 `getAuthentication()` 仅当用户尚未选择提供商(MVPD)且尚未进行身份验证时，才执行此操作。 的 `mvpds` 参数是可供用户使用的提供程序数组。
   - [&#39;setAuthenticationStatus(status， reason)&#39;](#$setAuthNStatus)

      - 触发者 `checkAuthentication()` 每次。 触发者 `getAuthentication()` 仅当用户已通过身份验证并选择了提供程序时。

      - 返回的状态已通过身份验证或未通过身份验证，原因描述身份验证失败或注销操作。
   - [navigateToUrl(url)](#$navigateToUrl)

      - 在AmazonFireOS SDK中忽略，该方法在由 `getAuthentication()` 用户选择MVPD后。  的 `url` 参数提供MVPD登录页面的位置。
   - [&#39;sendTrackingData(event， data)&#39;](#$sendTrackingData)

      - 触发者 `checkAuthentication(), getAuthentication(), checkAuthorization(), getAuthorization(), setSelectedProvider()`.
的 `event` 参数指示发生了哪个授权事件； `data` 参数是与事件相关的值列表。 
   - [&#39;setToken(token， resource)&#39;](#$setToken)

      - 触发者 `checkAuthorization()` 和 `getAuthorization()` 成功授权查看资源后。
      - 的 `token` 参数是短期媒体令牌； `resource` 参数是用户有权查看的内容。
   - [&#39;tokenRequestFailed(resource， code， description)&#39;](#$tokenRequestFailed)

      - 触发者 `checkAuthorization()` 和 `getAuthorization()` 授权失败后。
      - 的 `resource` 参数是用户尝试查看的内容；the `code` 参数是指示发生哪种类型的故障的错误代码；the `description` 参数描述与错误代码关联的错误。
   - [“selectedProvider(mvpd)”](#$selectedProvider)

      - 触发者 `getSelectedProvider()`.
      - 的 `mvpd` 参数提供有关用户选择的提供程序的信息。
   - [&#39;setMetadataStatus(metadata， key， arguments)&#39;](#$setMetadataStatus)

      - 触发者 `getMetadata().`
      - 的 `metadata` 参数提供您请求的特定数据；the `key` 参数是 `getMetadata()` 请求；和 `arguments` 参数是传递到的相同词典 `getMetadata()`.
   - [&#39;preauthorizedResources(resources)&#39;](#$preauthResources)

      - 触发者 `checkPreauthorizedResources()`.
      - 的 `authorizedResources` 参数显示用户有权查看的资源。\
          










![](assets/android-entitlement-flows.png)\
 

### B.启动流程 {#startup_flow}

1. 启动高级应用程序。
1. 启动Adobe Primetime身份验证
   1. 调用 [`getInstance`](#$getInstance) 创建Adobe Primetime身份验证AccessEnabler的单个实例。

      - **依赖关系：** Adobe Primetime身份验证本机Amazon FireOS库(AccessEnabler)
   2. 调用` setRequestor()` 确定程序员的身份；程序员的通行证 `requestorID` 和（可选）Adobe Primetime身份验证端点数组。

      - **依赖关系：** 有效的Adobe Primetime身份验证请求者ID(请与您的Adobe Primetime身份验证客户经理合作以安排此事。)

      - **触发器：** setRequestorComplete()回调

   在请求者身份完全建立之前，无法完成授权请求。 这实际上意味着，尽管setRequestor()仍在运行，但所有后续授权请求(例如，`checkAuthentication()`)。

   您有两个实施选项：请求者标识信息被发送到后端服务器后，UI应用层可以选择以下两种方法之一：</p>

   1. 等待触发 `setRequestorComplete()` callback（AccessEnabler委托的一部分）。  此选项最确定地 `setRequestor()` 已完成，因此建议在大多数实施中使用。

   1. 继续，而不等待触发 `setRequestorComplete()` 回调，并开始发出授权请求。 这些调用（checkAuthentication、checkAuthorization、getAuthentication、getAuthorization、checkPreauthorizedResource、getMetadata、注销）由AccessEnabler库排队，该库将在 `setRequestor()`. 例如，如果网络连接不稳定，此选项有时可能会中断。




1. 调用 [checkAuthentication()](#$checkAuthN) 来检查现有的身份验证，而不启动完整的身份验证流程。  如果此调用成功，您可以直接转到授权流程。  如果没有，请继续执行身份验证流程。

- **依赖关系：** 成功调用 `setRequestor()` （此依赖项也适用于所有后续调用）。

- **触发器：** setAuthenticationStatus()回调

### C.认证流程 {#authn_flow}

1. 调用 [`getAuthentication()`](#$getAuthN) 启动身份验证流程，或获取用户已经进行身份验证的确认。 

   **触发器：**  

   - setAuthenticationStatus()回调（如果用户已通过身份验证）。  在这种情况下，请直接转到 [授权流程](#authz_flow).
   - 如果用户尚未进行身份验证，则显示ProviderDialog()回调。  

1. 向用户显示发送到的提供程序列表 `displayProviderDialog()`.

1. 用户选择提供程序后，WebView将打开提供程序页面以供用户登录

   **注意：** 此时，用户有机会取消身份验证流程。 如果发生这种情况， AccessEnabler将清除其内部状态并重置身份验证流。

1. 用户成功登录后，WebView将关闭。

1. 调用 `getAuthenticationToken(),` 指示AccessEnabler从后端服务器检索身份验证令牌。 

1. [可选] 调用 [`checkPreauthorizedResources(resources)`](#$checkPreauth) 检查用户有权查看的资源。 的 `resources` 参数是与用户的身份验证令牌关联的受保护资源数组。\
   **触发器：** `preAuthorizedResources()` 回调\
   **执行点：** 在完成身份验证流程之后

1. 如果身份验证成功，请转到授权流程。

 

### D.授权流程 {#authz_flow}

1. 调用 [`getAuthorization()`](#$getAuthZ) 启动授权流程。

   依赖关系：与MVPD商定的有效资源ID。

   **注意：** ResourceID应当与在任何其他设备或平台上使用的ID相同，并且在MVPD中也将相同。

1. 验证身份验证和授权。

   - 如果 `getAuthorization()` 调用成功：用户具有有效的AuthN和AuthZ令牌（用户已通过身份验证并有权观看请求的媒体）。
   - 如果 `getAuthorization()` 失败：检查引发的异常以确定其类型（AuthN、AuthZ或其他内容）：
      - 如果是身份验证(AuthN)错误，则重新启动身份验证流程。
      - 如果是授权(AuthZ)错误，则用户无权观看请求的媒体，应向用户显示某种错误消息。
      - 如果存在其他类型的错误（连接错误、网络错误等） 然后向用户显示相应的错误消息。

1. 验证短媒体令牌。

   使用Adobe Primetime身份验证媒体令牌验证器库来验证从 `getAuthorization()` 上述调用：

   - 如果验证成功：为用户播放请求的媒体。
   - 如果验证失败：AuthZ令牌无效，应拒绝媒体请求，并向用户显示错误消息。

1. 返回到正常的应用程序流程。

### E.查看媒体流量 {#media_flow}

1. 用户选择要查看的媒体。
1.  介质是否受保护？  您的应用程序会检查所选介质是否受到保护：
   - 如果选定的介质受到保护，应用程序将启动 [授权流程](#authz_flow) 上。
   - 如果所选媒体未受保护，则为用户播放该媒体。

### F.注销流程 {#logout_flow}

1. 调用 [`logout()`](#$logout) 将用户注销。 \
   AccessEnabler清除用户在通过单点登录共享登录的所有请求方上为当前MVPD获取的所有缓存值和令牌。 清除缓存后， AccessEnabler会发起服务器调用以清理服务器端会话。  请注意，由于服务器调用可能导致到IdP的SAML重定向（这允许在IdP端清理会话），因此此调用必须遵循所有重定向。 因此，此调用将在WebView控件中处理，用户不可见。

   **注意：** 注销流程与验证流程不同，因为用户无需以任何方式与WebView交互。 因此，可以（并且建议）使WebView控件不可见(例如：隐藏)。

