---
title: AccessEnabler iOS/tvOS 3.7.0升级路径
description: AccessEnabler iOS/tvOS 3.7.0升级路径
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---


# AccessEnabler iOS/tvOS 3.7.0升级路径 {#accessenabler-iostvos-370-upgrade-path}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

</br>

密钥链存储更改 [新的AccessEnabler 3.7.0版](/help/authentication/authn-rn-ios-tvos-370.md) 与低于3.7.0版本的AccessEnabler中的密钥链存储实施不兼容。

采用新AccessEnabler 3.7.0版的一个应用程序的升级路径将迁移所有来自Keychain存储先前版本的令牌。 因此，最终用户 **不应丢失身份验证/授权会话** 在AccessEnabler框架更新过程中。

## 已知限制

实施人员可能会遇到以下某些限制。


1. 常规(Adobe)SSO在使用AccessEnabler 3.7.0版的一个应用程序和使用低于3.7.0版的AccessEnabler的一个应用程序之间不起作用，甚至对于由同一供应商开发的应用程序也是如此。

   - **重要信息：**
      - 系统级别(Apple)SSO将不会受到影响！
      - 如果两个应用程序都由同一供应商开发，并且使用低于3.7.0的AccessEnabler版本，则常规(Adobe)SSO将继续工作！
      - 如果两个应用程序都由同一供应商开发，并且使用AccessEnabler 3.7.0版，则常规(Adobe)单点登录(SSO)将可正常使用！

1. 如果使用AccessEnabler 3.7.0版将一个应用程序降级到较低版本的AccessEnabler，则不会迁移新生成的令牌。 因此，最终用户可能会遇到身份验证/授权会话丢失的情况，而不需要。

   - **重要信息：**
      - 通过系统级别(Apple)SSO验证的最终用户将不会受到影响！
      - 在使用AccessEnabler 3.7.0版更新到新应用程序之前已通过身份验证的最终用户不会受到影响！

1. 如果使用AccessEnabler 3.7.0版将一个应用程序降级到较低版本的AccessEnabler，则删除的令牌将不被确认。 因此，最终用户可能会遇到身份验证/授权会话的存在，而不需要它。
