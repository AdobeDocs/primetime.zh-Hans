---
title: 错误报告
description: 错误报告
exl-id: a52bd2cf-c712-40a2-a25e-7d9560b46ba6
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '2961'
ht-degree: 1%

---

# 错误报告 {#error-reporting}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权的使用。


## 概述 {#overview}

Adobe Primetime身份验证中的错误报告当前通过两种不同的方式实现：

* **高级错误报告** 如果出现以下情况，实施人员会注册错误回调 [AccessEnabler JavaScript SDK](#accessenabler-javascript-sdk) 或实现名为&#39;&#39;的Interface方法`status`”如果是 [AccessEnabler iOS/tvOS SDK](#accessenabler-ios-tvos-sdk) 和 [AccessEnabler Android SDK](#accessenabler-android-sdk)，以便接收高级错误报告。 错误分为 **信息**， **警告**、和 **错误** 类型。 此报告系统是 **异步**，在此 **无法保证触发多个错误的顺序**.  有关高级错误报告系统的详细信息，请参阅 [高级错误报告](#advanced-error-reporting) 部分。

* **原始错误报告 —** 一种静态报告系统，当特定请求失败时，会将错误消息传递给特定的回调函数。 错误分为通用、身份验证和授权类型。 有关原始系统中报告的错误列表，请参见 [原始错误报告](#original-error-reporting) 部分。


## 高级错误报告 {#advanced-error-reporting}

* [AccessEnabler JavaScript SDK](#accessenabler-javascript-sdk)
* [AccessEnabler iOS/tvOS SDK](#accessenabler-ios-tvos-sdk)
* [AccessEnabler Android SDK](#accessenabler-android-sdk)
* [AccessEnabler FireOS SDK](#accessenabler-fireos-sdk)

>[!IMPORTANT]
>
>旧的 [原始错误报告](#original-error-reporting) API将继续像以前一样工作，高级错误报告不会破坏功能，但原始错误报告将不再接收任何更新。 所有新的错误和更新都将发生在高级错误报告系统中。

### AccessEnabler JavaScript SDK {#accessenabler-javascript-sdk}

新的错误报告系统是可选的，因此，实施者可以显式注册错误处理程序回调以接收高级错误报告。 该系统包括动态注册和取消注册多个错误回调的能力。 此外，加载AccessEnabler JavaScript SDK后，您可以立即注册任何新的错误回调，而无需执行任何其他初始化（在调用之前） `setRequestor()`)，这意味着您能够接收有关初始化和配置错误的高级报告。


#### 实现 {#access-enab-js-imp}

yourErrorHandler(errorData：Object)


您的错误处理程序回调函数将接收具有以下结构的单个对象（映射）：

```JavaScript
    {
      errorId: "CFG410",
      level: "error",
      message: "This a fancy message",  // Optional
      .
      .                                 // Optional key/value pairs
      .
    }
```

### 1.绑定 {#bind}

**`.bind(eventType:String, handlerName:String):void`**

附加事件的处理程序。

**`eventType`**  — 仅&#39;&#39;`errorEvent`“ ”值导致AccessEnabler JavaScript SDK触发高级错误报告回调。

**`handlerName`**  — 一个字符串，它指定错误处理程序函数的名称。\
 

两个绑定参数必须只使用以下集中的字符： `[0-9a-zA-Z][-._a-zA-Z0-9]`；即，参数必须以数字或字母开头，然后只能包含连字符、句点、下划线和字母数字字符。  此外，参数不能超过1024个字符。  

**示例** 绑定错误处理程序的：

```JavaScript
accessEnabler.bind('errorEvent', 'myCustomErrorHandler');
accessEnabler.bind('errorEvent', 'errorLogger');
```

由于技术限制，您无法绑定关闭或匿名函数。 必须在第二个参数中指定方法的名称。

 
### 2.解除绑定 {#unbind}

**`.unbind(eventType:String, handlerName:String=null):void`**

删除以前附加的事件处理程序。

**`eventType`**  — 仅&#39;`errorEvent`&#39;值导致AccessEnabler JavaScript SDK触发高级错误报告回调。

**`handlerName`**  — 一个字符串，指定错误处理程序函数的名称（如果为null或缺少指定函数的所有附加处理程序） `eventType` 将被删除。

两个绑定参数必须只使用以下集中的字符： `[0-9a-zA-Z][-._a-zA-Z0-9]`；即，参数必须以数字或字母开头，然后只能包含连字符、句点、下划线和字母数字字符。  此外，参数不能超过1024个字符。  

**示例** 删除单个错误处理程序时：

`accessEnabler.unbind('errorEvent', 'errorLogger');`

**示例** 删除所有错误处理程序：

`accessEnabler.unbind('errorEvent');`


### AccessEnabler iOS/tvOS SDK {#accessenabler-ios-tvos-sdk}

新的错误报告系统是强制性的，因此，实施者必须明确遵守新的Objective C“EntitlementStatus”协议。 这种新方法允许程序员接收高级错误报告。

#### 实现 {#accessenab-ios-tvossdk-imp}

实施者需要符合以下要求 **权利状态** 协议：

**EntitlementStatus.h**

```OBJ-C
    #import <Foundation/Foundation.h>
     
    @protocol EntitlementStatus <NSObject>
    - (void)status:(NSDictionary *)statusDictionary;
    @end
```

您的 **状态** 函数将接收单个对象(一个 `NSDictionary`)，具有以下结构：

```OBJ-C
    {
          errorId: "CFG410",
          level: "error",
          message: "This a fancy message",  // Optional
      .
      .                                 // Optional key/value pairs
      .
    }
```

**1. 声明**

```OBJ-C
    @interface MyEntitlementStatusDelegate : NSObject <EntitlementStatus>
```

**2. 实现**

```OBJ-C
    @implementation DemoAppAppDelegate     
    // very simple implementation
    - (void)status:(NSDictionary *)statusDict {
        NSLog(@"%@:\n%@", statusDict[@"level"], statusDict);
    }
```


### AccessEnabler Android SDK {#accessenabler-android-sdk}

新的错误报告系统是强制性的，因为实施者必须明确遵守 `IAccessEnablerDelegate` 接口定义的协议。 这种新方法允许程序员接收高级错误报告。

#### 实现 {#access-enablr-androidsdk-imp}

实施人员需要处理新的 `status` 接口中的方法`IAccessEnablerDelegate`. 此 **`status`** 函数将收到一个 **`AdvancedStatus`** 对象具有以下模型：

```C++
    class AdvancedStatus {
    
    String id; // Not Null
    String level; // Not Null
    String message; // Might be null
    String resource; // Might be null

    AdvancedStatus(String id, String level, String message, String resource) {
        this.id = id;
        this.level = level;
        this.message = message;
        this.resource = resource;
    } 
    
    //other private/public methods
    }
```

**示例**

```C++
    @Override
    public void status(AdvancedStatus advancedStatus) {
        String status = "status(" + advancedStatus.id + ", " + advancedStatus.level + ", " + advancedStatus.message + ", " + advancedStatus.resource + ")";
    
        Log.i(LOG_TAG, status);
    }
```

### AccessEnabler FireOS SDK {#accessenabler-fireos-sdk}


新的错误报告系统是强制性的，因为实施者必须明确遵守 `IAccessEnablerDelegate` 接口定义的协议。 这种新方法允许程序员接收高级错误报告。

#### 实现 {#access-enab-fireos-sdk-}

实施人员需要处理新的 `status`接口中的方法`IAccessEnablerDelegate`. 此 **`status`** 函数将收到一个 **`AdvancedStatus`** 对象具有以下模型：

```C++
    class AdvancedStatus {
    
    String id; // Not Null
    String level; // Not Null
    String message; // Might be null
    String resource; // Might be null

    AdvancedStatus(String id, String level, String message, String resource) {
        this.id = id;
        this.level = level;
        this.message = message;
        this.resource = resource;
    } 
    
    //other private/public methods
    }
```

**示例**

```C++
    @Override
    public void status(AdvancedStatus advancedStatus) {
        String status = "status(" + advancedStatus.id + ", " + advancedStatus.level + ", " + advancedStatus.message + ", " + advancedStatus.resource + ")";
    
        Log.i(LOG_TAG, status);
    }
```

## 高级错误代码参考 {#advanced-error-codes-reference}

下表列出并描述了新版错误API公开的错误代码，以及建议采取的更正操作：

| ID | 级别 | 描述 | 开发人员操作 | 用户操作 | JavaScript | iOS/tvOS | Android |
|---|-------------|------------|----------------|---|---|---|---|
| AAPL和AAPL_ERROR | 错误 | 通用Apple SSO错误 | 该错误包含带有原始VSA错误的详细信息字段。 | 不适用 | 不适用 | 是 | 不适用 |
| VSA203 | 信息 | 由于通过平台SSO登录，用户决定注销应用程序，而发生身份验证。 | 指示/提示用户从tvOS上的“设置” — >“帐户” — >“电视提供商”中明确注销。 <br><br> 指示/提示用户从iOS/iPadOS上的“设置” — >“电视提供商”中明确注销。 | 从tvOS上的“设置” — >“帐户” — >“电视提供商”中明确注销。 <br> <br> 从iOS/iPadOS上的“设置” — >“电视提供商”中明确注销 | 不适用 | 是 | 不适用 |
| VSA404 | 信息 | 应用程序视频订户帐户权限未确定。 | 通过解释单点登录(SSO)用户体验的好处，激励拒绝授予访问订阅信息权限的用户。 | 用户可通过以下方式更改其决定：转到应用程序设置（访问电视提供商），或转到iOS/iPadOS上的“设置” — >“电视提供商”或tvOS上的“设置” — >“帐户” — >“电视提供商”部分。 | 不适用 | 是 | 不适用 |
| VSA503 | 信息 | 应用程序视频订阅者帐户元数据请求失败。 | MVPD端点没有响应。 应用程序可以回退到常规的身份验证流程。 | 不适用 | 不适用 | 是 | 不适用 |
| 500 | 错误 | 内部错误 | 使用AccessEnablerDebug和检查调试日志（console.log输出）以确定哪里出了问题。 | 不适用 | 是 | 是 | 不适用 |
| SEC403 | 错误 | 域安全错误。 请求者正在使用无效域。 特定请求者ID使用的所有域需要按Adobe列入白名单。 |  — 仅从允许的域列表中加载AccessEnabler <br> <br>  — 联系Adobe以管理所用请求者ID的域白名单 <br> <br> - iOS：验证您使用的证书是否正确，以及是否正确创建了签名 | 不适用 | 不适用 | 是 | 不适用 |
| SEC412 | 警告 | [ 在2.5版中提供 ] 设备ID不匹配。 每当基础平台更改其设备ID时，就会发生这种情况。 在这种情况下，将清除现有令牌，并且用户将不再进行身份验证。 请注意，当用户使用JS SDK并漫游时（在JS上，客户端IP是设备ID的一部分），这种情况是合法的。 否则，这可能表示存在欺诈企图 — 尝试从其他设备复制令牌。 |  — 监视警告数。 如果它们没有明显的原因（没有最近的浏览器更新；新的操作系统）而激增，这可能表明存在欺诈行为。  <br> <br> — （可选）通知用户需要重新登录。 | 再次登录。 | 是 | 是 | 3.2中的是 |
| SEC420 | 错误 | 与Adobe Primetime身份验证服务器通信时出现HTTP安全错误。 此错误通常在设置欺骗/代理时发生。 |  — 加载 `[https://]{SP_FQDN\}` 并手动接受SSL证书，例如， **https://api.auth.adobe.com** 或 **https://api.auth-staging.adobe.com** <br> <br> — 将代理证书标记为受信任 | 如果这种情况发生在普通用户身上，则表明可能存在中间人攻击！ | 是 | 是 | 3.2中的是 |
| CFG100 | 警告 | 客户端计算机日期/时间/时区设置不正确。 这可能会导致身份验证/授权错误。 |  — 通知用户设置正确的时间。 <br> <br> 采取措施防止权利流动，因为权利流动很可能会失败。 | 设置正确的日期/时间。 | 是 | 是 | 3.2中的是 |
| CFG400 | 错误 | 提供了无效的请求者ID。 | 开发人员必须指定有效的请求者ID。 | 不适用 | 是 | 是 | 3.2中的是 |
| CFG404 | 错误 | 未找到Adobe Primetime身份验证服务器。 这种情况可能会在3种情况下发生： <br><br>  — 开发人员实施了无效的欺骗。 <br><br>  — 用户存在网络问题，无法访问Adobe Primetime身份验证域。 <br><br> -Adobe Primetime身份验证服务器配置错误。 <br><br>  **注意：** 在Firefox上，将显示CFG400，而不是CFG404（浏览器限制） |  — 检查欺骗。 <br><br>  — 检查网络/DNS设置。 <br><br>  — 通知Adobe。 | 检查网络/DNS设置。 | 是 | 是 | 3.2中的是 |
| CFG410 | 错误 | AccessEnabler太旧。 | 通知用户清除缓存。 | 清除浏览器缓存。 | 是 | 不适用 | 3.2中的是 |
| CFG5xx | 错误 | Adobe Primetime身份验证服务器遇到内部错误。 xx可以是任意数字。 |  — 通知Adobe Primetime身份验证不可用。 <br><br>  — 绕过Adobe Primetime身份验证。 <br> <br>  — 通知Adobe。 | 请稍后再试。 | 是 | 是 | 3.2中的是 |
| N000 | 信息 | 用户未经过身份验证。 | 不适用 | 登录。 | 是 | 是 | 3.2中的是 |
| N001 | 信息 | 在后台启动被动身份验证尝试。 对于配置有“每个请求者的身份验证”的MVPD，将出现这种情况。 虽然用户有望自动进行身份验证，但这会导致初始化时出现性能损失。 | （可选）通知用户或显示UI以提醒用户“工作正在进行中”。 | 等等。 | 是 | 是 | 3.2中的是 |
| N003 | 信息 | 用户从Apple MVPD选取器中选择“其他电视提供商”选项。 | 此 *displayProviderDialog* 将调用callback，应用程序可以回退到常规身份验证流程。 | 选择常规MVPD并继续使用登录屏幕。 | 不适用 | 是 | 不适用 |
| N004 | 信息 | 用户选择当前请求者不支持的电视节目提供商。 | 此 *displayProviderDialog* 将调用callback，应用程序可以回退到常规身份验证流程。 | 选择常规MVPD并继续使用登录屏幕。 | 不适用 | 是 | 不适用 |
| N005 | 信息 | 已取消MVPD选取器。 | 不适用 | 不适用 | 是 | 是 | 3.2中的是 |
| N010 | 警告 | 在为选定的MVPD设置全部身份验证降级规则时，对用户进行了身份验证。 | （可选）告知用户由于MVPD问题，他获得“免费”免费访问。 | 不适用 | 是 | 是 | 3.2中的是 |
| N011 | 信息 | 用户已使用TempPass进行身份验证。 |  — 通知用户。 <br> <br>  — 可以选择提供常规MVPD的列表。 | （可选）使用常规MVPD登录。 | 是 | 是 | 3.2中的是 |
| N111 | 警告 | TempPass已过期。 |  — 通知用户。 <br> <br>  — 提供常规MVPD列表。 <br> <br>  — 隐藏“临时传递”选项。 | 使用常规MVPD登录。 | 是 | 是 | 3.2中的是 |
| N130 | 错误 | **在会话中未找到身份验证令牌。**  这可能是由于以下原因之一造成的： <br> <br> 1. 浏览器已禁用（第三方） Cookie（不适用于AccessEnabler JavaScript SDK版本4.x） <br> <br> 2. 浏览器已启用“阻止跨站点跟踪”(Safari 11+) <br> <br> 3. 会话已过期 <br> <br> 4. 程序员连续不正确地调用身份验证API <br> <br> 注意：此错误代码不适用于全页重定向身份验证流程。 | 1.提示用户启用（第三方） Cookie <br> <br> 2. 提示用户禁用跨站点跟踪 <br> <br> 3. 提示用户重新进行身份验证 <br> <br> 4. 按正确的顺序调用API | 1.启用（第三方） Cookie <br> <br> 2. 禁用跨站点跟踪 <br> <br> 3. 重新进行身份验证 <br> <br> 4. 不适用 | 是 | 是 | 3.2中的是 |
| N500 | 错误 | 内部错误。 <br> <br> 注意：这是原始错误系统的“一般身份验证错误”和“内部身份验证错误”。 此错误最终将被逐步消除。 | 使用AccessEnablerDebug和检查调试日志（console.log输出）以确定哪里出了问题。 | 不适用 | 是 | 是 | 不适用 |
| R401 | 错误 | 尝试获取访问令牌时出错。 <br> <br> 注意：这是一个无法恢复的错误。 通知用户应用程序不可用。 | - iOS：检查应用程序中的软件语句和自定义方案。 <br> <br> - JavaScript：检查网站应用程序中的软件语句。 <br> <br> 使用Zendesk打开票证，并通知用户系统暂时不可用 | 不适用 | 是（从v4.0） | 是（从v3.0） | 3.2中的是 |
| R400 | 错误 | 应用程序未注册。 软件语句无效或已被撤销。 <br> <br> 注意：这是一个无法恢复的错误。 通知用户应用程序不可用。 | - iOS：检查应用程序中的软件语句和自定义方案。 <br> <br> - JavaScript：检查网站应用程序中的软件语句。 <br> <br> 使用Zendesk打开票证，并通知用户系统暂时不可用 | 不适用 | 是（从v4.0） | 是（从v3.0） | 3.2中的是 |
| REG500 | 错误 | 无法从服务器获取注册码。 <br> <br> 注意：这是一个无法恢复的错误。 通知用户应用程序不可用。 | 使用Zendesk打开票证，并通知用户系统暂时不可用。 | 不适用 | 是（从v4.0） | 是（从v3.0） | 3.2中的是 |
| REGCODE | 成功 | 在tvOS平台上名为setSelectedProvider API的应用程序。 | 指示/提示用户使用第二设备（屏幕）使用提供的注册码登录。 | 在第2台设备（屏幕）上使用regcode启动身份验证。 | 不适用 | 是，仅适用于tvOS | 不适用 |
| Z010 | 警告 | 在为选定的MVPD实施authenticate-all或authorize-all降级规则时，用户已获得授权。 | （可选）告知用户由于MVPD问题，他获得“免费”免费访问。 | 不适用 | 是 | 是 | 3.2中的是 |
| Z011 | 信息 | 用户已使用TempPass获得授权 | （可选）通知用户 | 不适用 | 是 | 是 | 3.2中的是 |
| Z100 | 错误 | 授权失败，因为用户没有对请求的资源的订阅，或者由于源自MVPD的其他原因，例如视频与用户帐户的家长控制设置不匹配 |  — 不允许播放。 <br> <br>  — 通知用户。 <br> <br>  — 错误消息中的“message”键可能包含由MVPD提供的更详细的消息。 | 不适用 | 是 | 是 | 3.2中的是 |
| Z110 | 错误 | 由于MVPD多次拒绝，授权被拒绝。 可能的欺诈企图或DOS。 |  — 不允许播放。 <br> <br>  — 通知用户。 | 不适用 | 是 | 是 | 3.2中的是 |
| Z120 | 错误 | 由于与MVPD通信的技术原因，授权被拒绝。 可能的网络错误。 |  — 不允许播放。 <br> <br>  — 通知用户MVPD遇到了困难，他们应该稍后再试。 | 请稍后再试。 | 是 | 是 | 3.2中的是 |
| Z130 | 错误 | 授权被拒绝，因为使用了无效/格式错误的资源。 | 检查资源字符串并进行更正。 通常，此错误是由于MRSS格式错误或使用纯字符串而不是MRSS所致。 | 不适用 | 是 | 是 | 3.2中的是 |
| Z169 | 错误 | 授权被拒绝，因为authzNone降级规则已应用于指定的资源。 | 通知用户 | 不适用 | 是 | 是 | 3.2中的是 |
| Z500 | 错误 | 内部错误。 <br> <br>  注意：这是旧版“一般身份验证错误”和“内部身份验证错误”。 此错误最终将被逐步消除。 | 使用AccessEnablerDebug和检查调试日志（console.log输出）以确定哪里出了问题。 | 不适用 | 是 | 是 | 3.2中的是 |
| P100 | 错误 | 预授权失败。 这很可能是由于请求授权的资源过多。 |  — 请勿使用超过允许的最大资源数。 <br> <br>  — 联系Adobe Primetime身份验证支持以查找/设置允许的最大资源数。 | 不适用 | 是（从v3.0） | 是 | 3.2中的是 |
| IS2XX | 错误 | 当个性化服务器终结点响应数据的格式无效或缺少所需的个性化信息时，将返回这些错误代码。 | 使用Zendesk打开票证，并通知用户系统暂时不可用 | 不适用 | 是（从v3.0） | 不适用 | 不适用 |
| IS4XX | 错误 | 如果个性化服务器终结点失败4XX — 是响应的HTTP状态代码，则会返回这些错误代码。 | 使用Zendesk打开票证，并通知用户系统暂时不可用 | 不适用 | 是（从v3.0） | 不适用 | 不适用 |
| IS5XX | 错误 | 如果个性化服务器终结点失败5XX — 是响应的HTTP状态代码，则会返回这些错误代码。 | 使用Zendesk打开票证，并通知用户系统暂时不可用 | 不适用 | 是（从v3.0） | 不适用 | 不适用 |
| IS0 | 错误 | 当个性化服务器端点完全没有响应，因此连接已超时时，将返回此代码 | 使用Zendesk打开票证，并通知用户系统暂时不可用 | 不适用 | 是（从v3.0） | 不适用 | 不适用 |
| LS011 | 警告 | 由于LSO/LocalStorage问题和WebStorage问题（或不可用）， AccessEnabler正在使用易失性存储。 <br> <br> 身份验证/授权不会持续超过当前页面！ 每次页面加载都会导致用户需要身份验证。 页面重新加载过程中不会强制执行配置的TTL。 |  — 通知用户限制。 <br> <br>  — 告知用户如何增加可用存储空间。 <br> <br>  — 或者注销以清除存储。 |  — 增加存储。 <br> <br>  — 注销以清除存储。 | 是 | 不适用 | 不适用 |

<br>

## 原始错误报告 {#original-error-reporting}

本节介绍原始错误报告系统以及原始错误代码。 在原始错误报告系统中，AccessEnabler将错误传递到这两个回调函数： `setAuthenticationStatus()` 在调用之后 `checkAuthentication()`； `tokenRequestFailed()`，在对的调用失败后 `checkAuthorization()` 或 `getAuthorization()`.

原始错误报告和状态API继续像之前一样工作。 但是，以后将不会更新原始错误报告API。 有关旧错误的所有新错误报告和更新将仅在新版本中反映 [高级错误报告系统](#advanced-error-reporting).


有关使用原始错误报告系统的示例，请参见 [JavaScript API参考](/help/authentication/javascript-sdk-api-reference.md)：[setAuthenticationStatus()](/help/authentication/javascript-sdk-api-reference.md#set-authn-status-isauthn-error) 和 [tokenRequestFailed()](/help/authentication/javascript-sdk-api-reference.md#token-request-failed-error-msg) 函数， [iOS/tvOS API参考](/help/authentication/iostvos-sdk-api-reference.md)： [setAuthenticationStatus()](/help/authentication/javascript-sdk-api-reference.md#setAuthNStatus)和 [tokentRequestFailed()](/help/authentication/javascript-sdk-api-reference.md#tokenReqFailed)， [Android API参考](/help/authentication/android-sdk-api-reference.md)： [setAuthenticationStatus()](/help/authentication/android-sdk-api-reference.md#setAuthNStatus) 和 [tokenRequestFailed()](/help/authentication/android-sdk-api-reference.md#setAuthNStatus#tokenRequestFailed).

### 原始回调错误代码 {#original-callback-error-codes}

| **一般错误** |  |
|---|---|
| 内部错误 | 尝试处理请求时发生系统错误。 |
| 未选择提供程序错误 | 当客户在提供商选择对话框中取消时发生。 |
| 提供程序不可用错误 | 当没有可用的提供程序时发生。 |
|  |  |
| **身份验证错误** |  |
| 一般身份验证错误 | 当原因未知或无法发布时返回。 |
| 内部身份验证错误 | 尝试进行身份验证时出现系统错误。 |
| 用户未验证错误 | 用户未经过身份验证。 |
|  |  |
| **授权错误** |  |
| 一般授权错误 | 当原因未知或无法发布时返回。 |
| 内部授权错误 | 尝试授权时出现系统错误。 |
| 用户未授权错误 | 客户无权查看请求的内容。 |

<!--
## Related Information {#related-information}

* [JavaScript API Reference](/help/authentication/javascript-sdk-api-reference.md)
* [iOS/tvOS API Reference](/help/authentication/iostvos-sdk-api-reference.md)
* **Android API Reference**
-->
