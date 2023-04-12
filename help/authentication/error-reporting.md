---
title: 错误报告
description: 错误报告
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '2961'
ht-degree: 1%

---

# 错误报告 {#error-reporting}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。


## 概述 {#overview}

Adobe Primetime身份验证中的错误报告当前采用两种不同的方式实施：

* **高级错误报告** 如果 [AccessEnabler JavaScript SDK](#accessenabler-javascript-sdk) 或实现名为“ ”的接口方法`status`“ [AccessEnabler iOS/tvOS SDK](#accessenabler-ios-tvos-sdk) 和 [AccessEnabler Android SDK](#accessenabler-android-sdk)，以接收高级错误报告。 错误分为 **信息**, **警告**&#x200B;和 **错误** 类型。 此报告系统 **异步**，在 **无法保证触发多个错误的顺序**.  有关高级错误报告系统的详细信息，请参阅 [高级错误报告](#advanced-error-reporting) 中。

* **原始错误报告 —** 一种静态报告系统，在该系统中，当特定请求失败时，错误消息会传递到特定回调函数。 错误分为通用、身份验证和授权类型。 有关在原始系统中报告的错误列表，请参阅 [原始错误报告](#original-error-reporting) 中。


## 高级错误报告 {#advanced-error-reporting}

* [AccessEnabler JavaScript SDK](#accessenabler-javascript-sdk)
* [AccessEnabler iOS/tvOS SDK](#accessenabler-ios-tvos-sdk)
* [AccessEnabler Android SDK](#accessenabler-android-sdk)
* [AccessEnabler FireOS SDK](#accessenabler-fireos-sdk)

>[!IMPORTANT]
>
>旧 [原始错误报告](#original-error-reporting) API将继续正常运行，高级错误报告不会中断功能，但原始错误报告将不再接收任何更新。 高级错误报告系统将发生所有新错误和更新。

### AccessEnabler JavaScript SDK {#accessenabler-javascript-sdk}

新的错误报告系统是可选的，因此实施者可以显式注册错误处理程序回调以接收高级错误报告。 该系统包括动态注册和注销多个错误回调的能力。 此外，在加载AccessEnabler JavaScript SDK后，您可以立即注册任何新的错误回调，而无需执行任何其他初始化（在调用之前） `setRequestor()`)，这意味着您能够接收有关初始化和配置错误的高级报告。


#### 实施 {#access-enab-js-imp}

yourErrorHandler(errorData:Object)


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

为事件附加处理程序。

**`eventType`**  — 仅“`errorEvent`&quot;值会导致AccessEnabler JavaScript SDK触发高级错误报告回调。

**`handlerName`**  — 指定错误处理程序函数名称的字符串。\
 

两个绑定参数必须只使用以下集中的字符： `[0-9a-zA-Z][-._a-zA-Z0-9]`;即，参数必须以数字或字母开头，然后只能包含连字符、句点、下划线和字母数字字符。  此外，参数不能超过1024个字符。  

**示例** 绑定错误处理程序：

```JavaScript
accessEnabler.bind('errorEvent', 'myCustomErrorHandler');
accessEnabler.bind('errorEvent', 'errorLogger');
```

由于技术限制，您无法绑定闭包或匿名函数。 必须在第二个参数中指定方法的名称。

 
### 2.解除绑定 {#unbind}

**`.unbind(eventType:String, handlerName:String=null):void`**

删除之前附加的事件处理程序。

**`eventType`**  — 仅“`errorEvent`“值会导致AccessEnabler JavaScript SDK触发高级错误报告回调。

**`handlerName`**  — 指定错误处理程序函数名称的字符串（如果为null或缺少指定的所有附加处理程序） `eventType` 将被删除。

两个绑定参数必须只使用以下集中的字符： `[0-9a-zA-Z][-._a-zA-Z0-9]`;即，参数必须以数字或字母开头，然后只能包含连字符、句点、下划线和字母数字字符。  此外，参数不能超过1024个字符。  

**示例** 删除单个错误处理程序：

`accessEnabler.unbind('errorEvent', 'errorLogger');`

**示例** 删除所有错误处理程序：

`accessEnabler.unbind('errorEvent');`


### AccessEnabler iOS/tvOS SDK {#accessenabler-ios-tvos-sdk}

新的错误报告系统是强制性的，因此实施者必须明确符合新的Objective C“授权状态”协议。 这种新方法允许程序员接收高级错误报告。

#### 实施 {#accessenab-ios-tvossdk-imp}

实施者需要符合以下条件 **权利状态** 协议：

**EntitlementStatus.h**

```OBJ-C
    #import <Foundation/Foundation.h>
     
    @protocol EntitlementStatus <NSObject>
    - (void)status:(NSDictionary *)statusDictionary;
    @end
```

您的 **状态** 函数将接收单个对象( `NSDictionary`)，其结构如下：

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

**2. 实施**

```OBJ-C
    @implementation DemoAppAppDelegate     
    // very simple implementation
    - (void)status:(NSDictionary *)statusDict {
        NSLog(@"%@:\n%@", statusDict[@"level"], statusDict);
    }
```


### AccessEnabler Android SDK {#accessenabler-android-sdk}

新的错误报告系统是强制性的，因为实施者必须明确符合 `IAccessEnablerDelegate` 接口定义协议。 这种新方法允许程序员接收高级错误报告。

#### 实施 {#access-enablr-androidsdk-imp}

实施者需要处理新 `status` 方法`IAccessEnablerDelegate`. 的 **`status`** 函数将收到 **`AdvancedStatus`** 具有以下模型的对象：

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


新的错误报告系统是强制性的，因为实施者必须明确符合 `IAccessEnablerDelegate` 接口定义协议。 这种新方法允许程序员接收高级错误报告。

#### 实施 {#access-enab-fireos-sdk-}

实施者需要处理新 `status`方法`IAccessEnablerDelegate`. 的 **`status`** 函数将收到 **`AdvancedStatus`** 具有以下模型的对象：

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

下表列出并描述了较新错误API公开的错误代码，以及要采取哪些措施来更正它们的建议：

| ID | 级别 | 描述 | 开发人员操作 | 用户操作 | JavaScript | iOS/tvOS | Android |
|---|-------------|------------|----------------|---|---|---|---|
| AAPL&amp; AAPL_ERROR | 错误 | 一般Apple SSO错误 | 该错误包含一个包含原始VSA错误的详细信息字段。 | n/a | n/a | 是 | n/a |
| VSA203 | 信息 | 当通过平台SSO登录导致身份验证发生时，用户决定注销应用程序。 | 指示/提示用户明确从tvOS上的“设置” — >“帐户” — >“电视提供商”注销。 <br><br> 指示/提示用户从iOS/iPadOS上的“设置” — >“电视提供商”中明确注销。 | 从tvOS上的“设置” — >“帐户” — >“电视提供商”明确注销。 <br> <br> 从iOS/iPadOS上的“设置”>“电视提供商”中明确注销 | n/a | 是 | n/a |
| VSA404 | 信息 | 应用程序视频订阅者帐户权限未确定。 | 通过解释单点登录(SSO)用户体验的好处，激励拒绝授予访问订阅信息权限的用户。 | 用户可以通过转到应用程序设置（电视提供商访问权限）或iOS/iPadOS上的“设置” — >“电视提供商”或“设置” — >“帐户” — >“电视提供商tvOS”中的部分来更改其决定。 | n/a | 是 | n/a |
| VSA503 | 信息 | 应用程序视频订阅者帐户元数据请求失败。 | MVPD端点没有响应。 应用程序可能回退到常规身份验证流程。 | n/a | n/a | 是 | n/a |
| 500 | 错误 | 内部错误 | 使用AccessEnablerDebug并检查调试日志（console.log输出），以确定出错的原因。 | n/a | 是 | 是 | n/a |
| SEC403 | 错误 | 域安全错误。 请求者使用的域无效。 特定请求者ID使用的所有域都需要按Adobe列入白名单。 |  — 仅从允许的域列表中加载AccessEnabler <br> <br>  — 联系Adobe，以管理所用请求者ID的域白名单 <br> <br> -iOS:验证您使用的证书是否正确，以及签名是否已正确创建 | n/a | n/a | 是 | n/a |
| SEC412 | 警告 | [ 在版本2.5中提供 ] 设备ID不匹配。 每当基础平台更改其设备ID时，都可能发生这种情况。 在这种情况下，将清除现有令牌，并且用户将不再进行身份验证。 请注意，当用户使用JS SDK并且正在漫游（在JS上，客户端IP是设备ID的一部分）时，这是合法发生的。 否则，这可能表示欺诈尝试，即尝试从其他设备复制令牌。 |  — 监控警告的数量。 如果这些流量没有明显原因而激增(最近没有更新浏览器；新操作系统)，这可能是欺诈企图的一个指标。  <br> <br> — （可选）告知用户他需要再次登录。 | 再次登录。 | 是 | 是 | 是，从3.2开始 |
| SEC420 | 错误 | 与Adobe Primetime身份验证服务器通信时出现HTTP安全错误。 当欺骗/代理就绪时，通常会发生此错误。 |  — 加载 `[https://]{SP_FQDN\}` 并手动接受SSL证书，例如 **https://api.auth.adobe.com** 或 **https://api.auth-staging.adobe.com** <br> <br> — 将代理证书标记为受信任 | 如果对于普通用户，这表示可能是中间人攻击！ | 是 | 是 | 是，从3.2开始 |
| CFG100 | 警告 | 未正确设置客户端计算机Date / Time / Timezone。 这可能会导致身份验证/授权错误。 |  — 通知用户设置正确的时间。 <br> <br> 采取措施防止权利流，因为它们很可能会失败。 | 设置正确的日期/时间。 | 是 | 是 | 是，从3.2开始 |
| CFG400 | 错误 | 提供了无效的请求者ID。 | 开发人员必须指定有效的请求者ID。 | n/a | 是 | 是 | 是，从3.2开始 |
| CFG404 | 错误 | 未找到Adobe Primetime身份验证服务器。 这可能在3个实例中发生： <br><br>  — 开发人员已实施无效的欺骗。 <br><br>  — 用户出现网络问题，无法访问Adobe Primetime身份验证域。 <br><br> -Adobe Primetime身份验证服务器配置错误。 <br><br>  **注意：** 在Firefox上，将显示CFG400而不是CFG404（浏览器限制） |  — 检查欺骗。 <br><br>  — 检查网络/DNS设置。 <br><br>  — 通知Adobe。 | 检查网络/DNS设置。 | 是 | 是 | 是，从3.2开始 |
| CFG410 | 错误 | AccessEnabler太旧。 | 通知用户清除缓存。 | 清除浏览器缓存。 | 是 | n/a | 是，从3.2开始 |
| CFG5xx | 错误 | Adobe Primetime身份验证服务器遇到内部错误。 xx可以是任何数字。 |  — 告知用户Adobe Primetime身份验证不可用。 <br><br>  — 绕过Adobe Primetime身份验证。 <br> <br>  — 通知Adobe。 | 稍后再试。 | 是 | 是 | 是，从3.2开始 |
| N000 | 信息 | 用户未进行身份验证。 | n/a | 登录。 | 是 | 是 | 是，从3.2开始 |
| N001 | 信息 | 已在后台启动被动身份验证尝试。 对于配置了“每个请求者的身份验证”的MVPD，会发生这种情况。 虽然用户有望自动进行身份验证，但这会在初始化时对性能造成影响。 | （可选）通知用户或显示UI以提醒用户“工作正在进行”。 | 等等。 | 是 | 是 | 是，从3.2开始 |
| N003 | 信息 | 用户从Apple MVPD选取器中选择“其他电视提供商”选项。 | 的 *displayProviderDialog* 将调用callback，并且应用程序可能会回退到常规身份验证流程。 | 选择常规MVPD并继续登录屏幕。 | n/a | 是 | n/a |
| N004 | 信息 | 用户选择当前请求者不支持的电视提供商。 | 的 *displayProviderDialog* 将调用callback，并且应用程序可能会回退到常规身份验证流程。 | 选择常规MVPD并继续登录屏幕。 | n/a | 是 | n/a |
| N005 | 信息 | 已取消MVPD选取器。 | n/a | n/a | 是 | 是 | 是，从3.2开始 |
| N010 | 警告 | 在为所选MVPD设置“authenticate-all”降级规则时，用户已通过身份验证。 | 或者，通知用户由于MVPD困难而“免费”访问。 | n/a | 是 | 是 | 是，从3.2开始 |
| N011 | 信息 | 用户已使用TempPass进行身份验证。 |  — 通知用户。 <br> <br>  — （可选）提供常规MVPD的列表。 | （可选）使用常规MVPD登录。 | 是 | 是 | 是，从3.2开始 |
| N111 | 警告 | 过期的TempPass。 |  — 通知用户。 <br> <br>  — 提供常规MVPD的列表。 <br> <br>  — 隐藏TempPass选项。 | 使用常规MVPD登录。 | 是 | 是 | 是，从3.2开始 |
| N130 | 错误 | **在会话中未找到身份验证令牌。**  这可能是由于以下原因之一所致： <br> <br> 1. 浏览器已禁用（第三方）Cookie（不适用于AccessEnabler JavaScript SDK版本4.x） <br> <br> 2. 浏览器已启用阻止跨站点跟踪（Safari 11及更高版本） <br> <br> 3. 会话已过期 <br> <br> 4. 程序员以不正确的顺序调用身份验证API <br> <br> 注意：此错误代码不适用于全页重定向身份验证流。 | 1.提示用户启用（第三方）Cookie <br> <br> 2. 允许用户禁用跨站点跟踪 <br> <br> 3. 提示用户重新验证身份 <br> <br> 4. 按正确顺序调用API | 1.启用（第三方）Cookie <br> <br> 2. 禁用跨站点跟踪 <br> <br> 3. 重新验证 <br> <br> 4. 不适用 | 是 | 是 | 是，从3.2开始 |
| N500 | 错误 | 内部错误。 <br> <br> 注意：这是原始错误系统的“一般身份验证错误”和“内部身份验证错误”。 这一错误最终将逐步消除。 | 使用AccessEnablerDebug并检查调试日志（console.log输出），以确定出错的原因。 | n/a | 是 | 是 | n/a |
| R401 | 错误 | 尝试获取访问令牌时出错。 <br> <br> 注意：这是一个无法恢复的错误。 告知用户应用程序不可用。 | -iOS:检查应用程序中的软件语句和自定义方案。 <br> <br> - JavaScript:检查您网站应用程序中的软件语句。 <br> <br> 使用Zendesk打开票证，并告知用户系统暂时不可用 | n/a | 是，从v4.0开始 | 是，从v3.0 | 是，从3.2开始 |
| R400 | 错误 | 未注册应用程序。 软件语句无效或已吊销。 <br> <br> 注意：这是一个无法恢复的错误。 告知用户应用程序不可用。 | -iOS:检查应用程序中的软件语句和自定义方案。 <br> <br> - JavaScript:检查您网站应用程序中的软件语句。 <br> <br> 使用Zendesk打开票证，并告知用户系统暂时不可用 | n/a | 是，从v4.0开始 | 是，从v3.0 | 是，从3.2开始 |
| REG500 | 错误 | 无法从服务器获取注册代码。 <br> <br> 注意：这是一个无法恢复的错误。 告知用户应用程序不可用。 | 使用Zendesk打开一个票证，并告知用户系统暂时不可用。 | n/a | 是，从v4.0开始 | 是，从v3.0 | 是，从3.2开始 |
| REGCODE | 成功 | tvOS平台上名为setSelectedProvider API的应用程序。 | 指示/提示用户使用提供的注册代码使用第二个设备（屏幕）登录。 | 使用第2台设备（屏幕）上的regcode启动身份验证。 | n/a | 仅适用于tvOS | n/a |
| Z010 | 警告 | 在为所选MVPD设置“authenticate-all”或“authorize-all”降级规则时，用户已获得授权。 | 或者，通知用户由于MVPD困难而“免费”访问。 | n/a | 是 | 是 | 是，从3.2开始 |
| Z011 | 信息 | 用户已使用TempPass获得授权 | （可选）通知用户 | n/a | 是 | 是 | 是，从3.2开始 |
| Z100 | 错误 | 授权失败，因为用户未订阅请求的资源，或者由于来自MVPD的其他原因（例如，视频与用户帐户的家长控制设置不匹配） |  — 不允许播放。 <br> <br>  — 通知用户。 <br> <br>  — 错误消息中的“消息”键可能包含MVPD提供的更详细的消息。 | n/a | 是 | 是 | 是，从3.2开始 |
| Z110 | 错误 | 由于MVPD拒绝而拒绝授权。 可能的欺诈企图或DOS。 |  — 不允许播放。 <br> <br>  — 通知用户。 | n/a | 是 | 是 | 是，从3.2开始 |
| Z120 | 错误 | 由于与MVPD通信的技术原因而拒绝授权。 可能的网络错误。 |  — 不允许播放。 <br> <br>  — 告知用户MVPD遇到了困难，他们应稍后再试。 | 稍后再试。 | 是 | 是 | 是，从3.2开始 |
| Z130 | 错误 | 由于使用了无效/格式错误的资源，授权被拒绝。 | 检查资源字符串并更正该字符串。 通常，此错误是由于格式不正确的MRSS或使用纯字符串而不是MRSS所致。 | n/a | 是 | 是 | 是，从3.2开始 |
| Z169 | 错误 | 由于已对指定资源应用了authzNone降级规则，因此授权被拒绝。 | 通知用户 | n/a | 是 | 是 | 是，从3.2开始 |
| Z500 | 错误 | 内部错误。 <br> <br>  注意：这是旧版“一般身份验证错误”和“内部身份验证错误”。 这一错误最终将逐步消除。 | 使用AccessEnablerDebug并检查调试日志（console.log输出），以确定出错的原因。 | n/a | 是 | 是 | 是，从3.2开始 |
| P100 | 错误 | 预授权失败。 这很可能是因为请求授权的资源过多。 |  — 请勿使用超过允许的最大资源数。 <br> <br>  — 联系Adobe Primetime身份验证支持人员以查找/设置允许的最大资源数。 | n/a | 是，从v3.0 | 是 | 是，从3.2开始 |
| IS2XX | 错误 | 当个性化服务器端点响应数据的格式无效或缺少所需的个性化信息时，将返回这些错误代码。 | 使用Zendesk打开票证，并告知用户系统暂时不可用 | n/a | 是，从v3.0 | n/a | n/a |
| IS4XX | 错误 | 如果个性化服务器端点失败4XX — 是响应的HTTP状态代码，则会返回这些错误代码。 | 使用Zendesk打开票证，并告知用户系统暂时不可用 | n/a | 是，从v3.0 | n/a | n/a |
| IS5XX | 错误 | 在个性化服务器端点失败5XX时，会返回这些错误代码 — 是响应的HTTP状态代码。 | 使用Zendesk打开票证，并告知用户系统暂时不可用 | n/a | 是，从v3.0 | n/a | n/a |
| IS0 | 错误 | 当个性化服务器端点根本没有响应时，将返回此代码，因此连接已超时 | 使用Zendesk打开票证，并告知用户系统暂时不可用 | n/a | 是，从v3.0 | n/a | n/a |
| LS011 | 警告 | 由于LSO/LocalStorage问题和WebStorage问题（或不可用）， AccessEnabler正在使用易失存储。 <br> <br> 身份验证/授权不会在当前页面之外继续存在！。 每次页面加载都会导致用户需要进行身份验证。 在重新加载页面时，不会强制使用已配置的TTL。 |  — 告知用户限制。 <br> <br>  — 告知用户如何增加可用存储空间。 <br> <br>  — 或者注销以清除存储。 |  — 增加存储。 <br> <br>  — 注销以清除存储。 | 是 | n/a | n/a |

<br>

## 原始错误报告 {#original-error-reporting}

本节介绍原始错误报告系统以及原始错误代码。 在原始错误报告系统中， AccessEnabler将错误传递到以下两个回调函数： `setAuthenticationStatus()` 调用 `checkAuthentication()`; `tokenRequestFailed()`，在调用失败后 `checkAuthorization()` 或 `getAuthorization()`.

原始错误报告和状态API将继续像以前一样工作。 但是，今后不会更新原始错误报告API。 所有有关旧错误的新错误报告和更新将仅反映在Newe中 [高级错误报告系统](#advanced-error-reporting).


有关使用原始错误报告系统的示例，请参阅 [JavaScript API参考](/help/authentication/javascript-sdk-api-reference.md):[setAuthenticationStatus()](/help/authentication/javascript-sdk-api-reference.md#set-authn-status-isauthn-error) 和 [tokenRequestFailed()](/help/authentication/javascript-sdk-api-reference.md#token-request-failed-error-msg) 函数， [iOS/tvOS API参考](/help/authentication/iostvos-sdk-api-reference.md): [setAuthenticationStatus()](/help/authentication/javascript-sdk-api-reference.md#setAuthNStatus)和 [tokentRequestFailed()](/help/authentication/javascript-sdk-api-reference.md#tokenReqFailed), [Android API参考](/help/authentication/android-sdk-api-reference.md): [setAuthenticationStatus()](/help/authentication/android-sdk-api-reference.md#setAuthNStatus) 和 [tokenRequestFailed()](/help/authentication/android-sdk-api-reference.md#setAuthNStatus#tokenRequestFailed).

### 原始回调错误代码 {#original-callback-error-codes}

| **一般错误** |  |
|---|---|
| 内部错误 | 尝试处理请求时发生系统错误。 |
| 未选择提供程序错误 | 在提供商选择对话框中客户取消时发生。 |
| 提供程序不可用错误 | 在没有提供程序时发生。 |
|  |  |
| **身份验证错误** |  |
| 一般身份验证错误 | 原因未知或无法发布时返回。 |
| 内部身份验证错误 | 尝试验证时出现系统错误。 |
| 用户未验证错误 | 用户未通过身份验证。 |
|  |  |
| **授权错误** |  |
| 一般授权错误 | 原因未知或无法发布时返回。 |
| 内部授权错误 | 尝试授权时出现系统错误。 |
| 用户未授权错误 | 客户无权查看请求的内容。 |

<!--
## Related Information {#related-information}

* [JavaScript API Reference](/help/authentication/javascript-sdk-api-reference.md)
* [iOS/tvOS API Reference](/help/authentication/iostvos-sdk-api-reference.md)
* **Android API Reference**
-->