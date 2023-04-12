---
title: JavaScript SDK指南
description: JavaScript SDK指南
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 0%

---


# JavaScript SDK指南 {#javascript-sdk-cookbook}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## 简介(#intro)

本文档介绍程序员的上级应用程序为与Adobe Primetime身份验证服务的JavaScript集成实施的权利工作流。 JavaScript API引用的链接包含在中。

另请注意， [相关信息](#related) 部分包含指向一组JavaScript代码示例的链接。

## 权利流(#entitlement)

1. [先决条件](#prereq)
2. [启动流程](#startup)
3. [身份验证流程](#authn)
4. [授权流程](#authz)
5. [查看媒体流量](#logout)

</br>

![](assets/javascript-flows.png)


## 先决条件(#prereq)

**依赖关系：**

- Adobe Primetime身份验证库(AccessEnabler)，请与您的Adobe Primetime身份验证客户经理合作来安排此操作。
- 有效的Adobe Primetime身份验证请求者ID，请与您的Adobe Primetime身份验证客户经理合作以安排此事。

创建回调函数：

- `entitlementLoaded`

</br>

**触发器：** AccessEnabler已加载并完成初始化。

- `displayProviderDialog(mvpds)`

   **触发器：** `getAuthentication(),` 仅当用户未选择提供程序(MVPD)且尚未进行身份验证时， mvpds参数才是可供用户使用的提供程序数组。

- `setAuthenticationStatus(status, errorcode)`

   **触发器：**
   - `checkAuthentication()`每次。
   - `getAuthentication()` 仅当用户已通过身份验证并选择了提供程序时。

   返回的状态是成功或失败；错误代码描述失败的类型。

- `createIFrame(width, height)`

   **触发器：** `setSelectedProvider(providerID)`，但前提是选定的提供程序配置为在IFrame中显示。

   >[!NOTE]
   >
   >提供者被配置为将其身份验证屏幕呈现为重定向或iFrame中的，并且程序员需要考虑这两者。

- `sendTrackingData(event, data)`

   **触发器：** `checkAuthentication(), getAuthentication(),checkAuthorization(), getAuthorization(), setSelectedProvider()`.  的 `event` 参数指示发生了哪个授权事件；the `data` 参数是与事件相关的值列表。 
- `setToken(token, resource)`

   **触发器：** `checkAuthorization()`和 `getAuthorization()` 成功授权查看资源后。   的 `token` 参数是短时的媒体令牌；the `resource` 参数是用户有权查看的内容。

- `tokenRequestFailed(resource, code, description)`

   **触发器：**`checkAuthorization()`&#x200B;和`getAuthorization()`  授权失败后。\
   的 `resource` 参数是用户尝试查看的内容；the `code` 参数是指示发生哪种类型的故障的错误代码；the `description` 参数描述与错误代码关联的错误。

- `selectedProvider(mvpd)`

   **触发器：** [`getSelectedProvider()`](#$getSelProv `mvpd` 参数提供有关用户选择的提供程序的信息。

- `setMetadataStatus(metadata, key, arguments)`

   **触发器：** `getMetadata().`\
   的 `metadata` 参数提供您请求的特定数据；key参数是 `getMetadata()`请求；和 `arguments` 参数是传递到的相同词典 `getMetadata()`.


## 2.启动流程

**I.加载AccessEnabler JavaScript:**

**对于暂存配置文件**

```JSON
<script type="text/javascript"         
src="https://entitlement.auth-staging.adobe.com/entitlement/v4/AccessEnabler.js">
</script>"
```

或……

**对于生产配置文件**

```JSON
<script type="text/javascript"         
src="https://entitlement.auth.adobe.com/entitlement/v4/AccessEnabler.js">
</script>"
```

**触发器：** 初始化完成后，Adobe Primetime身份验证会调用 `entitlementLoaded()` 回调函数。 这是应用程序与AccessEnabler通信的入口点。 

 
**二。** 调用 `setRequestor()`确定程序员的身份；程序员的通行证 `requestorID` 和（可选）Adobe Primetime身份验证端点数组。

**触发器：** 无，但启用 `displayProviderDialog()` 在需要时被调用。


**三。** 调用 `checkAuthentication()` 检查现有身份验证，而不启动完整 [验证流程].  如果此调用成功，您可以直接转到 `authorization flow`.  如果没有，请继续 `authentication flow`.

**依赖关系：** 成功调用 `setRequestor()`（此依赖项也适用于所有后续调用）。

 **触发器：** `setAuthenticationStatus()` 回调

</br>

## 3.身份验证流程</span>


**依赖关系：** 成功调用 `setRequestor()`（此依赖项也适用于所有后续调用）。


调用 `getAuthentication()` 以获取身份验证状态OR以触发提供程序身份验证流程。

**触发器：**

- `displayProviderDialog()`如果用户尚未进行身份验证
- `setAuthenticationStatus()` 如果已进行身份验证

当AccessEnabler调用时，验证流程即会完成 `setAuthenticationStatus()`with `isAuthenticated == 1`.

## 4.授权流程(#authz)

**依赖关系：**

- 成功调用 `setRequestor()` （此依赖项也适用于所有后续调用）。
- 与MVPD商定的有效资源ID。 请注意，ResourceIDs应当与在任何其他设备或平台上使用的ID相同，并且在MVPD中也将相同。

调用 `getAuthorization()` 并传递所请求媒体的ResourceID。 成功的调用将返回短媒体令牌，该令牌确认用户有权查看请求的媒体。

- 如果调用通过：用户具有有效的AuthN令牌，且用户有权观看请求的媒体。
- 如果调用失败：检查引发的异常以确定其类型（AuthN、AuthZ或其他内容）：
- 如果调用是AuthN错误，则重新启动AuthN流。
- 如果调用是AuthZ错误，则用户无权观看请求的媒体，应向用户显示某种错误消息。
- 如果存在其他错误（连接错误、网络错误等） 然后向用户显示相应的错误消息。

使用媒体令牌验证器验证从成功 `getAuthorization()` 呼叫。

 
**依赖关系：** 短媒体令牌验证器（随AccessEnabler库一起提供）

- 如果验证通过：显示/播放用户请求的媒体。
- 如果失败：AuthZ令牌无效，应拒绝媒体请求，并向用户显示错误消息。

## 5.查看媒体流(#logout)

- 用户选择要查看的媒体。
   - 介质是否受保护？\
           — 您的应用程序检查媒体是否受到保护：
      - 如果媒体受到保护，则您的应用程序将启动上述授权(AuthZ)流程。
      - 如果介质未受保护，请继续查看介质流。
      - 播放媒体

## 配置访客ID(#visitorID)

配置 [Experience CloudvisitorID](https://marketing.adobe.com/resources/help/en_US/mcvid/) 从分析的角度来看，值非常重要。 设置EC visitorID值后，SDK将随每次网络调用发送此信息，Adobe Primetime身份验证服务将收集此信息。 这样，您就能够将来自Adobe Primetime身份验证服务的分析数据与来自其他应用程序或网站的任何其他分析报表相关联。 有关如何设置EC访客ID的信息可以找到 [此处](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=en).

 
>[!NOTE]
>
>请注意，从JS SDK版本3.1.0开始，便提供了此功能支持。 

<!--
### Related Information (#related)

* [JavaScript SDK Overview](/help/authentication/javascript-sdk-overview.md)
* [JavaScript SDK API Reference](/help/authentication/javascript-sdk-api-reference.md)
* **JavaScript SDK Code Samples**
-->