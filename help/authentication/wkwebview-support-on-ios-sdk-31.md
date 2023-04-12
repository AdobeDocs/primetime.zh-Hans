---
title: iOS SDK 3.1+上的WKWebView支持
description: iOS SDK 3.1+上的WKWebView支持
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---


# iOS SDK 3.1+上的WKWebView支持 {#wkwebview-support-on-ios-sdk-3.1}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

</br>

**由于Apple在iOS上弃用UIWebView，我们更新了iOS SDK 3.1，以支持WKWebView。**

## 兼容性 {#compatibility}

从iOS SDK版本3.1开始，实施人员现在可以交替使用WKWebView或UIWebView。 由于Apple已弃用UIWebView，因此应用程序应该迁移到WKWebView，以避免将来的iOS版本出现问题。

请注意，迁移只需使用WKWebView切换UIWebView类即可，在Adobe的AccessEnabler方面没有具体工作要做。

## 已知问题 {#known-issues}

Adobe的AccessEnabler使用隐藏的内部UIWebView实例来执行“[被动认证](/help/authentication/sso-passive-authn.md)”。 “被动”流对于需要对每个请求者ID进行身份验证的MVPD非常有用，而通过此流，在多个iOS应用程序中使用相同团队ID以模拟SSO体验(AdobeSSO)的程序员受益匪浅。 当前，有限数量的MVPD使用此功能。

该功能使用UIWebView的行为，该行为允许Adobe捕获身份验证Cookie并在“被动”流程中重播它们。 WKWebView引入了更强大的安全性，可阻止Adobe捕获登录时设置的Cookie，并使用WKWebView的隐藏实例重播它们。 由于这一安全性改进，并且考虑到在非常具体的实施场景中，“被动”流只使一组非常有限的MVPD受益（多个应用程序使用相同的团队ID），因此，Adobe删除了使用Webview进行身份验证的MVPD的“被动身份验证”功能。

该功能仍适用于配置为使用SFSafariViewController的MVPD，但请注意，在这种情况下，用户将可看到“被动”身份验证，因为SFSafariViewController无法以“隐藏”方式使用。
