---
title: Cookie更新 — SameSite和安全标记
description: Cookie更新 — SameSite和安全标记
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 0%

---



# Cookie更新 — SameSite和安全标记 {#cookies-updates---samesite-and-secure-flags}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

</br>


## 更新 {#Updates}

本部分重点介绍Chrome浏览器和Adobe Primetime身份验证为处理第三方Cookie而引入的更改。

 

### Chrome 80更新 {#Chrome}

从Chrome版本80（版本82除外）开始，未指定 *SameSite* 属性会被视为 *SameSite=Lax*. 因此，需要在跨站点上下文中传送的Cookie必须明确指定 *SameSite=None*，且还必须使用 *安全* 属性和提交 *HTTPS*. 有关这些更新的更多详细信息，请参阅官方的chromium页面： <https://www.chromium.org/updates/same-site> 也来自 <https://web.dev/samesite-cookies-explained/>.


### Adobe Primetime身份验证更新 {#Pass-Updates}

Adobe Primetime身份验证服务当前依赖于一些从浏览器的角度来看被视为第三方Cookie的Cookie（包括Chrome），以便能够与某些平台和版本的Adobe Primetime身份验证SDK结合使用。 因此，为了符合即将发生的更改，并继续在来自这些旧版SDK的跨站点上下文中交付这些Cookie，Adobe Primetime身份验证服务会在 *adobe-pass-2.55.1* 版本。

这些更改来自 *adobe-pass-2.55.1* 版本涉及添加 *安全* 和 *SameSite=None* 属性。当使用以版本80及更高版本（版本82除外）开始的Chrome浏览器时，该属性用于其传递回所有Adobe Primetime身份验证SDK的所有Cookie。

下一部分介绍当一个用户使用Chrome浏览器80及更高版本（版本82除外）时，平台和Adobe Primetime身份验证SDK版本列表存在的一些潜在问题。

## 疑难解答 {#Troubleshooting}

浏览此部分时，请记住所有Adobe Primetime身份验证服务Cookie必须 *安全* 属性集 *adobe-pass-2.55.1* 版本，而 *SameSite=None* 必须仅为Chrome浏览器版本80及更高版本（版本82除外）设置属性。


### 一般疑难解答 {#General}

1. 请务必注意，一些用户代理已知与 *SameSite=None* 属性。

   - 从Chrome 51到Chrome 66的Chrome版本（两端包含）。 这些Chrome版本将拒绝 *SameSite=None*. 这还会影响旧版Chromium派生的浏览器以及Android WebView。 根据当时Cookie规范的版本，此行为是正确的，但是，在规范中添加了新的“无”值后，此行为已在Chrome 67及更高版本中更新。 (在Chrome 51之前，完全忽略SameSite属性，并且所有Cookie都会被视为 *SameSite=None*.)
   - Android上UC浏览器版本低于12.13.2。旧版本将拒绝使用的Cookie *SameSite=None*. 根据当时Cookie规范的版本，此行为是正确的，但是，在规范中添加了新的“无”值后，此行为已在较新版本的UC浏览器中更新。
   - MacOS 10.14上的Safari和嵌入式浏览器版本，以及iOS 12上的所有浏览器版本。 这些版本会错误地处理标有 *SameSite=None* 就象是标记了 *SameSite=Strict*. 已在较新版本的iOS和MacOS上修复此错误。


1. 请注意，Cookie具有 *安全* 属性必须发送 *HTTPS*，否则Cookie将无法访问Adobe Primetime身份验证服务。

   - AccessEnabler JavaScript SDK:
      - 强制要求与 *sp.auth.adobe.com* 使用 *HTTPS* 对于版本 *2.35* 和 *3.5.0*，然后再引入动态客户端注册。
   - AccessEnabler iOS/tvOS SDK:
      - 强制要求与 *sp.auth.adobe.com* 使用 *HTTPS* 对于以前的版本 *3.0.0*，然后再引入动态客户端注册。
   - AccessEnabler Android SDK:
      - 强制要求与 *sp.auth.adobe.com* 使用 *HTTPS* 对于以前的版本 *3.0.0*，然后再引入动态客户端注册。
   - AccessEnabler FireOS SDK:
      - 强制要求与 *sp.auth.adobe.com* 使用 *HTTPS* 对于版本 *2.0.4*.

</br>

### AccessEnabler JavaScript SDK版本2.35疑难解答 {#235-Troubleshooting}

在Chrome 80及更高版本（版本82除外）中，用户的身份验证流程可能会受到影响。 为了确保用户不因上述更新而出现身份验证问题，可以：

- 检查 *JSESSIONID* cookie在浏览器中设置，并具有 *SameSite=None* 和 *安全* 属性集。 
- 检查 *JSESSIONID* cookie *https://sp.auth.adobe.com/authenticate/saml* 网络请求与 *JSESSIONID* cookie *https://sp.auth.adobe.com/session* 网络请求。


### AccessEnabler JavaScript SDK版本3.5.0疑难解答 {#350-Troubleshooting}

在Chrome 80及更高版本（版本82除外）中，用户的身份验证流程可能会受到影响。 为了确保用户不因上述更新而出现身份验证问题，可以：

- 检查 *JSESSIONID* cookie在浏览器中设置，并具有 *SameSite=None* 和 *安全* 属性集。 
- 检查 *JSESSIONID* cookie *https://sp.auth.adobe.com/authenticate/saml* 网络请求与 *JSESSIONID* cookie *https://sp.auth.adobe.com/session* 网络请求。
- 检查 *pass\_sfp* cookie在浏览器中设置，并具有 *SameSite=None* 和 *安全* 属性集。
- 检查 *pass\_sfp* cookie在 *https://sp.auth.adobe.com/session* 网络请求。


在Chrome 80及更高版本（版本82除外）中，用户的授权流程可能会受到影响。 为了确保用户在观看受保护的资源时不会遇到问题，在成功进行身份验证后，由于上述更新，用户可以：

- 检查 *pass\_sfp* cookie在浏览器中设置，并具有 *SameSite=None* 和 *安全* 属性集。
- 检查 *pass\_sfp* cookie在 *https://sp.auth.adobe.com/adobe-services/authorize* 网络请求。
- 检查 *pass\_sfp* cookie在 *https://sp.auth.adobe.com/adobe-services/shortAuthorize* 网络请求。
