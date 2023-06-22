---
title: Amazon FireOS集成指南
description: Amazon FireOS集成指南
exl-id: 1982c485-f0ed-4df3-9a20-9c6a928500c2
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '1433'
ht-degree: 0%

---

# Amazon FireOS集成指南 {#amazon-fireos-integration-cookbook}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权的使用。

</br>


## 介绍 {#intro}

本文档描述了程序员的上层应用程序可以通过Amazon FireOS AccessEnabler库公开的API实施的授权工作流。

Amazon FireOS的Adobe Primetime身份验证权利解决方案最终分为两个域：

- UI域 — 这是上层应用程序层，它实施UI并使用AccessEnabler库提供的服务来提供对受限内容的访问。
- AccessEnabler域 — 这是权利工作流的实施形式：
   - 向Adobe后端服务器发出的网络调用
   - 与身份验证和授权工作流相关的业务逻辑规则
   - 各种资源的管理和工作流状态的处理（如令牌缓存）

AccessEnabler域的目标是隐藏授权工作流的所有复杂内容，并（通过AccessEnabler库）向上层应用程序提供一组用于实施授权工作流的简单授权基元：

1. 设置请求者身份
1. 检查并获取针对特定身份提供者的身份验证
1. 检查并获取特定资源的授权
1. 注销

AccessEnabler的网络活动发生在不同的线程中，因此从不阻止UI线程。 因此，两个应用程序域之间的双向通信信道必须遵循完全异步模式：

- UI应用层通过AccessEnabler库公开的API调用将消息发送到AccessEnabler域。
- AccessEnabler通过UI层向AccessEnabler库注册的AccessEnabler协议中包含的回调方法响应UI层。

## 权利流 {#entitlement}

1. [先决条件](#prereqs)
1. [启动流程](#startup_flow)
1. [身份验证流程](#authn_flow)
1. [授权流程](#authz_flow)
1. [查看媒体流](#media_flow)
1. [注销流程](#logout_flow)

 

### A.先决条件 {#prereqs}

1. 创建回调函数：
   - [&#39;setRequestorComplete()&#39;](#$setRequestorComplete)

      - 触发者 `setRequestor()`，返回成功或失败。     成功表示您可以继续权利调用。
   - [displayProviderDialog(mvpd)](#$displayProviderDialog)

      - 触发者 `getAuthentication()` 仅当用户尚未选择提供程序(MVPD)且尚未进行身份验证时。 此 `mvpds` parameter是用户可用的提供程序数组。
   - [&#39;setAuthenticationStatus(status， reason)&#39;](#$setAuthNStatus)

      - 触发者 `checkAuthentication()` 每次。 触发者 `getAuthentication()` 仅当用户已经过身份验证并已选择提供商时。

      - 返回的状态是经过身份验证还是未经身份验证，原因描述了身份验证失败或注销操作。
   - [navigateToUrl(url)](#$navigateToUrl)

      - 在AmazonFireOS SDK中忽略，方法在Android平台上使用，触发平台为 `getAuthentication()` 在用户选择MVPD之后。  此 `url` 参数提供MVPD登录页面的位置。
   - [&#39;sendTrackingData(event， data)&#39;](#$sendTrackingData)

      - 触发者 `checkAuthentication(), getAuthentication(), checkAuthorization(), getAuthorization(), setSelectedProvider()`.
此 `event` 参数指示发生的权利事件； `data` parameter是与事件相关的值的列表。 
   - [&#39;setToken(token， resource)&#39;](#$setToken)

      - 触发者 `checkAuthorization()` 和 `getAuthorization()` 成功授权查看资源后。
      - 此 `token` 参数是短期媒体令牌；而 `resource` 参数是用户有权查看的内容。
   - [&#39;tokenRequestFailed(resource， code， description)&#39;](#$tokenRequestFailed)

      - 触发者 `checkAuthorization()` 和 `getAuthorization()` 授权失败后。
      - 此 `resource` 参数是用户尝试查看的内容； `code` 参数是错误代码，指示发生了什么类型的失败； `description` 参数描述与错误代码关联的错误。
   - [&#39;selectedProvider(mvpd)&#39;](#$selectedProvider)

      - 触发者 `getSelectedProvider()`.
      - 此 `mvpd` 参数提供有关用户选择的提供程序的信息。
   - [&#39;setMetadataStatus(metadata， key， arguments)&#39;](#$setMetadataStatus)

      - 触发者 `getMetadata().`
      - 此 `metadata` 参数提供您请求的特定数据； `key` 参数是中使用的键 `getMetadata()` 请求；以及 `arguments` 参数是传递到的相同字典 `getMetadata()`.
   - [&#39;preauthorizedResources（资源）&#39;](#$preauthResources)

      - 触发者 `checkPreauthorizedResources()`.
      - 此 `authorizedResources` 参数表示用户有权查看的资源。\
          










![](assets/android-entitlement-flows.png)\
 

### B.启动流程 {#startup_flow}

1. 启动上层应用程序。
1. 启动Adobe Primetime身份验证
   1. 调用 [`getInstance`](#$getInstance) 创建一个Adobe Primetime身份验证AccessEnabler实例。

      - **依赖关系：** Adobe Primetime身份验证本机Amazon FireOS库(AccessEnabler)
   2. 调用` setRequestor()` 建立程序员身份，传给程序员 `requestorID` 和（可选）Adobe Primetime身份验证端点数组。

      - **依赖关系：** 有效的Adobe Primetime身份验证请求者ID(请与Adobe Primetime身份验证客户经理合作安排此过程。)

      - **触发器：** setRequestorComplete()回调

   在完全建立请求者身份之前，无法完成任何授权请求。 这实际上意味着setRequestor()仍在运行时，所有后续权利请求(例如，`checkAuthentication()`)被阻止。

   您有两个实施选项：在将请求者标识信息发送到后端服务器后，UI应用程序层可以选择以下两种方法之一：</p>

   1. 等待触发 `setRequestorComplete()` callback（AccessEnabler委托的一部分）。  此选项最能确定 `setRequestor()` 已完成，因此建议在大多数实施中使用该选项。

   1. 继续操作，无需等待触发 `setRequestorComplete()` 回调，并开始发出授权请求。 这些调用(checkAuthentication、checkAuthorization、getAuthentication、getAuthorization、checkPreauthorizedResource、getMetadata、logout)由AccessEnabler库排队，该库将在 `setRequestor()`. 例如，如果网络连接不稳定，则此选项有时可能会中断。




1. 调用 [checkAuthentication()](#$checkAuthN) 检查现有身份验证，而不启动完整的身份验证流程。  如果此调用成功，您可以直接进入授权流程。  如果不能，请继续进入身份验证流程。

- **依赖关系：** 成功调用了 `setRequestor()` （此依赖关系也适用于所有后续调用）。

- **触发器：** setAuthenticationStatus()回调

### C.身份验证流程 {#authn_flow}

1. 调用 [`getAuthentication()`](#$getAuthN) 启动身份验证流程，或获取用户已进行身份验证的确认。 

   **触发器：**  

   - setAuthenticationStatus()回调（如果用户已经过身份验证）。  在这种情况下，请直接转到 [授权流程](#authz_flow).
   - displayProviderDialog()回调（如果用户尚未进行身份验证）。  

1. 向用户显示已发送到的提供商列表 `displayProviderDialog()`.

1. 用户选择提供程序后，WebView将打开提供程序页面供用户登录

   **注意：** 此时，用户有机会取消身份验证流程。 如果发生这种情况，AccessEnabler将清理其内部状态并重置身份验证流程。

1. 用户成功登录后，WebView将关闭。

1. 调用 `getAuthenticationToken(),` 它会指示AccessEnabler从后端服务器检索身份验证令牌。 

1. [可选] 调用 [`checkPreauthorizedResources(resources)`](#$checkPreauth) 以检查用户有权查看哪些资源。 此 `resources` parameter是与用户的身份验证令牌关联的受保护资源数组。\
   **触发器：** `preAuthorizedResources()` callback\
   **执行点：** 完成身份验证流程后

1. 如果身份验证成功，请转到授权流。

 

### D.授权流程 {#authz_flow}

1. 调用 [`getAuthorization()`](#$getAuthZ) 以启动授权流。

   依赖项：与MVPD商定的有效ResourceID。

   **注意：** ResourceID应该与任何其他设备或平台上使用的相同，并且在MVPD中应该是相同的。

1. 验证身份验证和授权。

   - 如果 `getAuthorization()` 调用成功：用户具有有效的AuthN和AuthZ令牌（用户已经过身份验证并有权观看请求的媒体）。
   - 如果 `getAuthorization()` 失败：检查引发的异常以确定其类型（AuthN、AuthZ或其他内容）：
      - 如果这是身份验证(AuthN)错误，则重新启动身份验证流程。
      - 如果这是授权(AuthZ)错误，则用户无权观看请求的媒体，应向用户显示某种错误消息。
      - 是否存在其他类型的错误（连接错误、网络错误等） 然后向用户显示相应的错误消息。

1. 验证短媒体令牌。

   使用Adobe Primetime身份验证媒体令牌验证器库验证从返回的短暂媒体令牌 `getAuthorization()` 调用：

   - 如果验证成功：为用户播放请求的媒体。
   - 如果验证失败： AuthZ令牌无效，应拒绝媒体请求，并向用户显示错误消息。

1. 返回到正常应用程序流程。

### E.查看媒体流 {#media_flow}

1. 用户选择要查看的媒体。
1.  媒体是否受保护？  您的应用程序会检查所选媒体是否受保护：
   - 如果所选媒体受保护，您的应用程序将启动 [授权流程](#authz_flow) 上面。
   - 如果所选媒体未受保护，则为用户播放该媒体。

### F.注销流程 {#logout_flow}

1. 调用 [`logout()`](#$logout) 以注销用户。 \
   AccessEnabler会清除用户为当前MVPD获取的所有缓存值和令牌，这些值和令牌位于共享单点登录的所有请求者上。 清除缓存后，AccessEnabler会进行服务器调用以清除服务器端会话。  请注意，由于服务器调用可能会导致到IdP的SAML重定向（这允许IdP端的会话清理），因此此调用必须在所有重定向之后进行。 因此，此调用将在WebView控件中处理，对用户不可见。

   **注意：** 注销流与身份验证流的不同之处在于，用户不需要以任何方式与WebView交互。 因此，可以（并且建议）在注销过程中隐藏WebView控件（即：隐藏）。
