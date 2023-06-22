---
title: Cookie更新 — SameSite和Secure标记
description: Cookie更新 — SameSite和Secure标记
exl-id: cc1f60fd-fa64-48cb-a185-dba562a54c33
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 0%

---

# Cookie更新 — SameSite和Secure标记 {#cookies-updates---samesite-and-secure-flags}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权的使用。

</br>


## 更新 {#Updates}

本节重点介绍Chrome浏览器和Adobe Primetime身份验证引入的用于处理第三方Cookie的更改。

 

### Chrome 80更新 {#Chrome}

从Chrome版本80（版本82除外）开始，未指定 *SameSite* 会将属性视为视为其在 *SameSite=Lax*. 因此，需要在跨站点上下文中交付的Cookie必须明确指定 *SameSite=None*，并且还必须使用 *安全* 属性和传递于 *HTTPS*. 有关这些更新的更多详细信息，请参阅chromium官方页面： <https://www.chromium.org/updates/same-site> 以及来自 <https://web.dev/samesite-cookies-explained/>.


### Adobe Primetime身份验证更新 {#Pass-Updates}

为了与某些平台和版本的Adobe Primetime Authentication SDK结合使用，Adobe Primetime Authentication Service当前依赖于从浏览器的角度被视为第三方Cookie的一对Cookie，包括Chrome。 因此，为了遵循即将到来的更改并在跨站点上下文中继续通过这些旧版SDK提供这些Cookie，Adobe Primetime身份验证服务将在中实施所需的更改 *adobe-pass-2.55.1* 版本。

这些更改来自 *adobe-pass-2.55.1* 版本涉及添加 *安全* 和 *SameSite=None* 使用从版本80及更高版本（版本82除外）开始的Chrome浏览器时，其所有Cookie的属性会传递回所有Adobe Primetime身份验证SDK。

下一部分将显示平台和Adobe Primetime Authentication SDK版本列表的一些潜在问题，以防一个用户使用Chrome浏览器80及更高版本（版本82除外）。

## 疑难解答 {#Troubleshooting}

浏览本节时，请记住，所有Adobe Primetime身份验证服务Cookie必须具有 *安全* 属性集于 *adobe-pass-2.55.1* 版本，而 *SameSite=None* 只能为Chrome浏览器版本80及更高版本（版本82除外）设置属性。


### 一般故障排除 {#General}

1. 需要注意的是，某些用户代理已知与 *SameSite=None* 属性。

   - 从Chrome 51到Chrome 66的Chrome版本（两端包含）。 这些Chrome版本将通过以下方式拒绝Cookie： *SameSite=None*. 这也会影响旧版本的Chromium派生浏览器以及Android WebView。 根据当时Cookie规范的版本，此行为是正确的，但是随着规范中新增的“无”值，此行为在Chrome 67及更高版本中已更新。 (在Chrome 51之前，SameSite属性被完全忽略，并且所有Cookie都被视为与以前一样 *SameSite=None*.)
   - Android上12.13.2版之前的UC浏览器版本。旧版本会拒绝具有以下功能的Cookie： *SameSite=None*. 根据当时Cookie规范的版本，此行为是正确的，但是随着规范中新增的“无”值，此行为已在较新版本的UC浏览器中更新。
   - macOS 10.14上的Safari和嵌入式浏览器的版本以及iOS 12上的所有浏览器。 这些版本将错误地处理标有 *SameSite=None* 好像它们被标记了 *SameSite=严格*. 此错误已在较新版本的iOS和MacOS上修复。


1. 需要注意的是，Cookie具有 *安全* 属性必须发送过 *HTTPS*，否则Cookie将无法访问Adobe Primetime身份验证服务。

   - AccessEnabler JavaScript SDK：
      - 强制要求与的通信 *sp.auth.adobe.com* 用途 *HTTPS* 版本 *2.35* 和 *3.5.0*，然后再开始动态客户端注册。
   - AccessEnabler iOS/tvOS SDK：
      - 强制要求与的通信 *sp.auth.adobe.com* 用途 *HTTPS* 适用于之前的版本 *3.0.0*，然后再开始动态客户端注册。
   - AccessEnabler Android SDK：
      - 强制要求与的通信 *sp.auth.adobe.com* 用途 *HTTPS* 适用于之前的版本 *3.0.0*，然后再开始动态客户端注册。
   - AccessEnabler FireOS SDK：
      - 强制要求与的通信 *sp.auth.adobe.com* 用途 *HTTPS* for version *2.0.4*.

</br>

### AccessEnabler JavaScript SDK版本2.35故障排除 {#235-Troubleshooting}

Chrome 80及更高版本（版本82除外）中可能会影响用户的身份验证流程。 为了确保用户不会因上述更新而遇到身份验证问题，可以：

- 检查 *JSESSIONID* Cookie在浏览器中设置，并具有 *SameSite=None* 和 *安全* 属性集。 
- 检查 *JSESSIONID* 来自的Cookie *https://sp.auth.adobe.com/authenticate/saml* 网络请求与 *JSESSIONID* 来自的Cookie *https://sp.auth.adobe.com/session* 网络请求。


### AccessEnabler JavaScript SDK版本3.5.0故障排除 {#350-Troubleshooting}

Chrome 80及更高版本（版本82除外）中可能会影响用户的身份验证流程。 为了确保用户不会因上述更新而遇到身份验证问题，可以：

- 检查 *JSESSIONID* Cookie在浏览器中设置，并具有 *SameSite=None* 和 *安全* 属性集。 
- 检查 *JSESSIONID* 来自的Cookie *https://sp.auth.adobe.com/authenticate/saml* 网络请求与 *JSESSIONID* 来自的Cookie *https://sp.auth.adobe.com/session* 网络请求。
- 检查 *pass\_sfp* Cookie在浏览器中设置，并具有 *SameSite=None* 和 *安全* 属性集。
- 检查 *pass\_sfp* Cookie设置于 *https://sp.auth.adobe.com/session* 网络请求。


Chrome 80及更高版本（版本82除外）中可能会影响用户的授权流程。 为了确保用户没有观看受保护资源的问题，在成功进行身份验证后，由于进行了上述更新，用户可以：

- 检查 *pass\_sfp* Cookie在浏览器中设置，并具有 *SameSite=None* 和 *安全* 属性集。
- 检查 *pass\_sfp* Cookie设置于 *https://sp.auth.adobe.com/adobe-services/authorize* 网络请求。
- 检查 *pass\_sfp* Cookie设置于 *https://sp.auth.adobe.com/adobe-services/shortAuthorize* 网络请求。
