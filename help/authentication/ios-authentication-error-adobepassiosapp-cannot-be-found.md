---
title: iOS身份验证错误 — 找不到adobepass.ios.app
description: iOS身份验证错误 — 找不到adobepass.ios.app
exl-id: cd97c6fb-f0fa-45c2-82c1-f28aa6b2fd12
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# iOS身份验证错误 — 找不到adobepass.ios.app {#ios-authentication-error-adobepass.ios.app-cannot-be-found}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权的使用。

## 问题 {#issue}

用户正在经历身份验证流程，在他们成功向提供商输入凭据后，他们会被重定向回错误页面、搜索页面或其他某个自定义页面，通知他们 `adobepass.ios.app` 找不到/无法解析。

## 说明 {#explanation}

在iOS上， `adobepass.ios.app` 用作最终重定向URL，以指示AuthN流已完成。 此时，应用程序需要向AccessEnabler发出请求，以获取身份验证令牌并完成身份验证流程。

问题是 `adobepass.ios.app` 不存在，并将在 `webView`. 旧版iOS DemoApp假定此错误始终会在AuthN流结束时触发，并设置为相应地处理它(`indidFailLoadWithError`)。

**注意：** 此问题已在DemoApp的更高版本(包含在iOS SDK下载中)中修复。

不幸的是，这一假设并不正确。 有一些所谓的“智能” DNS或代理服务器不会简单地传递出现的错误，而是会执行以下操作之一： 

- 创建自定义错误页面
- 转发到搜索页面或某些其他类型的客户页面或门户。

在这些情况下，返回到iOS webView的响应将是对webView而言完全有效的响应，并且不会触发旧DemoApp所依赖的错误。

## 解决方案 {#solution}

不要做出与DemoApp相同的假设。 相反，在执行请求之前截获该请求(在 `shouldStartLoadWithRequest`)，并正确处理它。

在执行请求之前截获请求的示例：

```obj-c
- (BOOL)webView:(UIWebView*)localWebView shouldStartLoadWithRequest:(NSURLRequest*)request navigationType:(UIWebViewNavigationType)navigationType {

NSString *absolutePath = [[request URL] absoluteString]; 
if ([absolutePath isEqualToString:ADOBEPASS_REDIRECT_URL] && ![APP_DELEGATE getAuthenticationWasCalled]) {

// user was logged ok => call getAuthenticationToken() 
[APP_DELEGATE setGetAuthenticationWasCalled:YES]; 
[[APP_DELEGATE accessEnabler] getAuthenticationToken];
return NO;

}

return YES;

}
```

需要注意以下几点：

- 从未使用 `adobepass.ios.app` 直接在代码中的任意位置访问。 改为使用常量 `ADOBEPASS_REDIRECT_URL`
- 此 `return NO;` 语句将阻止加载页面
- 绝对要确保 `getAuthenticationToken` 调用在您的代码中只调用一次。 多次调用 `getAuthenticationToken` 将导致未定义的结果。
