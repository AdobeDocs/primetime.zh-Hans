---
title: iOS/tvOS v3.x迁移指南
description: iOS/tvOS v3.x迁移指南
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---


# iOS/tvOS v3.x迁移指南 {#iostvos-v3x-migration-guide}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

>[!TIP]
> 
> **注意：**
>
> - 从iOS sdk 3.1版开始，实施人员现在可以交替使用WKWebView或UIWebView。 由于UIWebView已弃用，因此应用程序应该迁移到WKWebView，以避免将来iOS版本出现问题。
> - 请注意，迁移只需使用WKWebView切换UIWebView类即可，在Adobe的AccessEnabler方面没有具体工作要做。


</br>

## 更新内部版本设置 {#update}

本版本包含以SWIFT语言编写的功能。 如果您的应用程序完全是Objective-C，则需要将Target内部版本设置中的“始终嵌入Swift标准库”复选框设置为“是”。 设置此选项后，Xcode会扫描您的应用程序中捆绑的框架，如果其中任何框架包含Swift代码，它会将相关库复制到您的应用程序包中。 如果不更新内部版本设置，您的应用程序可能会崩溃，并出现错误，指出它无法加载AccessEnabler.framework或各种 `ibswift*` 库。

</br>

## 添加软件声明 {#add}

> 有关如何获取软件声明的信息，请转到此
> 页面：
> [申请注册](/help/authentication/iostvos-application-registration.md)

一旦您有了软件声明，我们建议将其托管在远程服务器上，这样您就可以轻松撤消或更改它，而无需在App Store中部署新版本的应用程序。 应用程序启动时，从远程位置获取软件语句，并在AccessEnabler构造函数中传递该语句：

```swift
    accessEnabler = AccessEnabler("YOUR_SOFTWARE_STATEMENT_HERE");
```

> 以下是API信息： [iOS / tvOS API参考](/help/authentication/iostvos-sdk-api-reference.md)

</br>

## 添加自定义URL方案 {#add-custom}

> 有关如何获取自定义URL方案的信息，请转到以下页面： [获取客户URL方案](/help/authentication/iostvos-application-registration.md)

获取自定义URL方案后，您需要将其添加到应用程序的info.plist文件中。 自定义方案具有以下格式： `adbe.u-XFXJeTSDuJiIQs0HVRAg://`. 将冒号和正斜杠添加到文件时，需要忽略它。 以上示例将 `adbe.u-XFXJeTSDuJiIQs0HVRAg`.

```plist
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>CUSTOM_URL_SCHEME_HERE</string>
            </array>
        </dict>
    </array>
```

</br>

## 在自定义URL方案中拦截调用 {#intercept}

仅当您的应用程序之前通过 [setOptions(\[&quot;handleSVC&quot;:true&quot;\])](/help/authentication/iostvos-sdk-api-reference.md) 为需要Safari View控制器(SVC)的特定MVPD调用和，因此需要由SFSafariViewController控制器而不是UIWebView/WKWebView控制器加载身份验证和注销端点的URL。

在验证和注销流程期间，您的应用程序必须监控 `SFSafariViewController `控制器进行多次重定向。 您的应用程序必须检测到加载由 `application's custom URL scheme` (例如，`adbe.u-XFXJeTSDuJiIQs0HVRAg://adobe.com)`. 当控制器加载此特定的自定义URL时，您的应用程序必须关闭 `SFSafariViewController` 并调用AccessEnabler的 `handleExternalURL:url `API方法。

在 `AppDelegate` 添加以下方法：

```swift
    func application(_ app: UIApplication, open url: URL, options: [UIApplicationOpenURLOptionsKey: Any]) -> Bool {
            if (url.absoluteString.hasPrefix("adbe.")) {
                accessEnabler.handleExternalURL(url.description)
                return true;
            } 
        }
```

> 以下是API信息： [处理外部URL](/help/authentication/iostvos-sdk-api-reference.md)

</br>

## 更新setRequestor方法签名 {#update-setreq}

由于新SDK使用的是新的身份验证机制，因此不需要signedRequestId参数或公钥和密钥（对于tvOS）。 的 `setRequestor` 方法得到简化，只需请求者ID。

### iOS

此代码：

```swift
    accessEnabler.setRequestor(requestorId, setSignedRequestorId: signedRequestorId)
```

变为：

```swift
    accessEnabler.setRequestor(requestorId)
```

</br>

### tvOS

此代码：

```swift
    accessEnabler.setRequestor(requestorId, setSignedRequestorId: signedRequestorId,
                    secret: "secret", publicKey: "public_key")
```

变为：

```swift
    accessEnabler.setRequestor(requestorId)
```

> 以下是API信息： [设置请求者](/help/authentication/iostvos-sdk-api-reference.md)

</br>

## 将getAuthenticationToken方法替换为handleExternalURL方法 {#replace}

`getAuthentication` 方法过去用于完成身份验证流程。 由于它的名称具有误导性，因此它被重命名为 `handleExternalURL` 和会将url作为参数。

更改以下所有情况：

```swift
    accessEnabler.getAuthenticationToken()
```

替换为：

```swift
    accessEnabler.handleExternalURL(request.url?.description);
```

> 以下是API信息： [处理外部URL](/help/authentication/iostvos-sdk-api-reference.md)
