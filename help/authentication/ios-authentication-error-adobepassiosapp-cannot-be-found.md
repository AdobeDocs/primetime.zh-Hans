---
title: iOS身份验证错误 — 找不到adobepass.ios.app
description: iOS身份验证错误 — 找不到adobepass.ios.app
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# iOS身份验证错误 — 找不到adobepass.ios.app {#ios-authentication-error-adobepass.ios.app-cannot-be-found}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## 问题 {#issue}

用户正在完成身份验证流程，在与提供商成功输入其凭据后，他们将被重定向回错误页面、搜索页面或其他一些自定义页面，以告知他们 `adobepass.ios.app` 找不到/解决。

## 说明 {#explanation}

在iOS, `adobepass.ios.app` 用作最终的重定向URL，以指示AuthN流已完成。 此时，应用程序需要向AccessEnabler发出请求，以获取AuthN令牌并完成AuthN流程。

问题是 `adobepass.ios.app` 实际上不存在，并且会在 `webView`. 旧版iOS DemoApp假定此错误将始终在AuthN流程结束时触发，并且经过设置以相应地处理(`indidFailLoadWithError`)。

**注意：** 在DemoApp的较新版本(随iOS SDK下载提供)中修复了此问题。

不幸的是，这一假设并不正确。 有些所谓的“智能”DNS或代理服务器不会简单地传递引发的错误，而是会执行下列操作之一： 

- 创建自定义错误页面
- 转发到搜索页面，或某些其他类型的客户页面或门户。

在这些情况下，返回到iOS webView的响应对于webView而言将是完全有效的响应，并且不会触发旧DemoApp所依赖的错误。

## 解决方案 {#solution}

请不要假定DemoApp会做出相同的假设。 相反，请在执行请求之前截获该请求(在 `shouldStartLoadWithRequest`)并正确处理。

有关如何在执行请求之前截获请求的示例：

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

请注意以下事项：

- 从不使用 `adobepass.ios.app` 代码中的任意位置。 请改用常量 `ADOBEPASS_REDIRECT_URL`
- 的 `return NO;` 语句将阻止页面加载
- 确保 `getAuthenticationToken` 调用在您的代码中只调用一次。 对 `getAuthenticationToken` 将产生未定义的结果。

