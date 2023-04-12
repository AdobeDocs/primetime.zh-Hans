---
title: 无刷新登录和注销
description: 无刷新登录和注销
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1772'
ht-degree: 0%

---


# 无刷新登录和注销 {#tefresh-less-login-and-logout}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## 概述 {#overview}

对于Web应用程序，您必须考虑一些不同的可能情况，以便对用户进行身份验证和注销。  MVPD要求用户登录MVPD的网页进行身份验证，同时还需要考虑以下其他因素：

- 某些MVPD需要从您的站点到其登录页面进行完全重定向
- 某些MVPD要求您在站点上打开iFrame以显示MVPD的登录页面
- 某些浏览器无法很好地处理iFrame方案，因此对于这些浏览器而言，更好的选择是使用弹出窗口而不是iFrame

在Adobe Primetime身份验证2.7之前，所有用于验证用户的情景都涉及程序员页面的完整页面刷新。对于2.7及后续版本，Adobe Primetime身份验证团队改进了这些流程，以便用户在登录和注销期间不必在您的应用程序上体验页面刷新。  


## 详细描述 {#detailed_description}

让我们从原始身份验证和注销流程的摘要开始，然后使用改进的身份验证和注销流程进行后续操作。 请注意，前四个部分针对的是正常的MVPD（非TempPass），而最后一部分则介绍需要用于TempPass的特殊实施：

- [原始身份验证流程](#orig_authn)
- [原始注销流程](#orig_logout)
- [改进了身份验证流程](#improved_authn)
- [改进了注销流程](#improved_logout)
- [TempPass流](#improved_temppass)

</br>

## 原始身份验证/注销流程 {#orig_authn}

**身份验证**

根据MVPD的要求，Adobe Primetime身份验证Web客户端有两种身份验证方式：

1. **整页重定向 —** 在用户从程序员网站上的MVPD选取器中选择提供商（配置了全页重定向）后， `setSelectedProvider(<mvpd>)` 将在AccessEnabler中调用，用户将被重定向到MVPD的登录页面。 在用户提供有效凭据后，会将他重定向回程序员网站。 AccessEnabler已初始化，并在验证期间从Adobe Primetime身份验证中检索身份验证令牌 `setRequestor`.
1. **iFrame/弹出窗口 —** 在用户选择提供程序（使用iFrame配置）后， `setSelectedProvider(<mvpd>)` 将在AccessEnabler中调用。 此操作将触发 `createIFrame(width, height)` 回调，通知程序员使用名称创建iFrame（或弹出窗口，具体取决于浏览器/首选项） `"mvpdframe"` 和提供的尺寸。 创建iFrame/popup后，AccessEnabler会在iFrame/popup中加载MVPD的登录页面。 用户提供有效凭据，并且iFrame/popup会被重定向到Adobe Primetime身份验证，该身份验证会返回一个JS代码段，该代码段会关闭iFrame/popup并重新加载父页面（程序员网站）。 与流程1类似，在 `setRequestor`. 

的 `displayProviderDialog` 回调(由 `getAuthentication`/`getAuthorization`)会返回MVPD及其相应设置的列表。 的 `iFrameRequired` MVPD的属性使程序员能够知道它应该激活流程1还是流程2。 请注意，程序员需要仅对流程2执行额外操作（创建iFrame/popup）。

**取消身份验证**

此外，用户还会通过关闭登录页面来明确取消身份验证流程。 以下是面向程序员的方案和建议的解决方案：

1. **整页重定向 —** 当登录页面关闭时，用户需要再次导航到程序员网站，并从头开始启动整个流程。 在这种情况下，程序员不需要采取明确的操作。
1. **iFrame -** 建议程序员在 `div` （或类似的UI组件），该组件上附加了“关闭”按钮。 当用户按下“关闭”按钮时，程序员将销毁iFrame以及关联的UI并执行 `setSelectedProvider(null)`. 此调用允许AccessEnabler清除其内部状态，并允许用户启动后续的身份验证流程。 `setAuthenticationStatus` 和 `sendTrackingData(AUTHENTICATION_DETECTION...)` 将触发，以指示身份验证流失败(两者均开启 `getAuthentication` 和 `getAuthorization`)。
1. **弹出窗口 —** 某些浏览器无法准确检测窗口关闭事件，因此需要在此采用不同的方法（与上面的iFrame流量相反）。 Adobe建议程序员初始化一个计时器，以定期验证登录弹出窗口是否存在。 如果窗口不存在，则程序员可以确保用户手动取消登录流程，并且程序员可以继续呼叫 `setSelectedProvider(null)`. 触发的回调与上面的流程2中的相同。

</br>

## 原始注销流程 {#orig_logout}

AccessEnabler的注销API清除库的本地状态，并在当前选项卡/窗口中加载MVPD的注销URL。 浏览器导航到MVPD的注销端点，该过程完成后，用户将被重定向回程序员网站。 代表用户需要的唯一操作是按“注销”按钮/链接并启动流程；在MVPD的注销端点上不需要用户交互。

**页面刷新时的原始身份验证/注销流程**

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/AE_with_refresh_web.png)

</br>

## 改进了（无刷新）身份验证 {#improved_authn}

>[!NOTE]
>
>改进的无刷新登录和注销流程要求浏览器支持包括Web消息传送在内的现代HTML5技术。

上面讨论的身份验证（登录）和注销流程在每个流程完成后重新加载主页，可提供相似的用户体验。  当前功能旨在通过提供无刷新（后台）登录和注销来改善用户体验。 程序员可以通过传递两个布尔标记(`backgroundLogin` 和 `backgroundLogout`) `configInfo` 参数 `setRequestor` API。 默认情况下，后台登录/注销处于禁用状态（这提供了与先前实施的兼容性）。

**示例：**

```JSON
    var configInfo = {
        callSetConfig: true,
        backgroundLogin: true,
        backgroundLogout: true
    };
    accessEnabler.setRequestor(REQUESTOR_ID, null, configInfo);
```

**身份验证**

以下几点描述了原始身份验证流和改进后的流之间的转换：

1. 全页重定向已替换为执行MVPD登录的新浏览器选项卡。 程序员需要创建新选项卡(通过 `window.open`)已命名 `mvpdwindow` 当用户选择MVPD( `iFrameRequired = false`)。 然后程序员执行 `setSelectedProvider(<mvpd>)`，允许AccessEnabler在新选项卡中加载MVPD登录URL。 在用户提供有效凭据后，Adobe Primetime身份验证将关闭选项卡，并向程序员网站发送window.postMessage，该网站向AccessEnabler发出验证流程已完成的信号。 触发了以下回调：

   - 如果流程是由 `getAuthentication`: `setAuthenticationStatus` 和 `sendTrackingData(AUTHENTICATION_DETECTION...)` 将触发，以表示身份验证成功/失败。

   - 如果流程是由 `getAuthorization`: `setToken/tokenRequestFailed` 和 `sendTrackingData(AUTHORIZATION_DETECTION...)` 将触发，以发出授权成功/失败的信号。

1. iFrame/弹出窗口流程基本保持不变，其区别在于用户提供有效凭据后，将不会重新加载父页面。 iFrame/弹出窗口将在登录后自动关闭，并且 `window.postMessage` 将发送到父页面，并通知AccessEnabler流程已完成。 与上一流程中一样触发相同的回调， **加上以下新回调： `destroyIFrame`**. 的 `destroyIFrame` callback允许程序员删除任何与iFrame关联的/辅助组件，如UI装饰。 旧身份验证流程中不需要存在此回调，因为登录完成后，Adobe Primetime身份验证将重新加载程序员页面，从而破坏该页面上的所有UI组件。

</br>     

>[!IMPORTANT]
> 
>必须将MVPD登录iFrame或弹出窗口作为包含AccessEnabler实例的页面的直接子项加载。 如果MVPD登录iFrame或弹出窗口在包含AccessEnabler实例的页面下方嵌套了两个或多个级别，则流程可能会挂起。 例如，如果主页和MVPD iFrame之间有一个iFrame（页面=\> iFrame =\> MVPD iFrame），则登录流程可能会失败。

</br>

 **取消身份验证**

以下是用于取消身份验证的流程：

1. **浏览器选项卡 —** 由于选项卡基本上是一个新窗口，因此捕获其关闭事件的限制与旧身份验证流程的场景3中讨论的限制相同。 此外，此处不可能使用计时器方法，因为无法区分用户手动关闭的选项卡和登录流程结束时自动关闭的选项卡。 此处的解决方案是，当用户取消流程时，AccessEnabler保持“静默”（不触发回调）。 此外，程序员不需要采取任何具体行动。 用户将能够启动另一个身份验证流程，而不会收到“多个身份验证请求错误”错误（此错误在AccessEnabler中已禁用后台登录）。

1. **iFrame -** 程序员可以采用情景2中所讨论的方法，从旧的身份验证流程（从iFrame创建包装器UI并触发关联的关闭按钮） `setSelectedProvider(null)`. 尽管此方法不再是一项强大要求（如上面的情景1中所述，允许多个身份验证流进行后台登录），但Adobe仍建议使用此方法。

1. **弹出窗口 —** 这与上面的浏览器选项卡流程相同。

</br>

## 改进了注销流程 {#improved_logout}

新的注销流程将在隐藏的iFrame中执行，从而消除整个页面重定向。  这是可能的，因为用户无需对MVPD注销页面执行特定操作。

注销流程完成后，它将将iFrame重定向到自定义Adobe Primetime身份验证端点。 这将提供执行 `window.postMessage` 向父代通知AccessEnabler注销已完成。 触发了以下回调： `setAuthenticationStatus()` 和 `sendTrackingData(AUTHENTICATION_DETECTION ...)`，表示用户不再进行身份验证。 

下图显示了无刷新流程，该流程允许用户在不刷新应用程序主页的情况下登录其MVPD:

**改进了（无刷新）身份验证/注销流程**

![](https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/images/AE_with_no_refresh_web.png)

</br>

## TempPass流 {#improved_temppas}

对于TempPass类型的MVPD，无刷新登录采用不同的方法。

由于TempPass流要求自动创建一个窗口，并且在没有明确用户交互的情况下关闭该窗口，因此它可能会对某些浏览器（弹出窗口阻止程序）造成问题。 因此，AccessEnabler在后台实施登录阶段，而不需要程序员创建的Web容器。

以下是在实施TempPass for Refresh-less登录和注销时程序员需要注意的方面：

- 在开始身份验证之前，只需为非TempPass MVPD创建iFrame或弹出窗口。 程序员可通过读取 `tempPass` MVPD对象的属性(由 `setConfig()` / `displayProviderDialog()`)。

- 的 `createIFrame()` 回调必须包含对TempPass的检查，并且仅当MVPD为NOT TempPass时才执行其逻辑。

- 的 `destroyIFrame()` 回调必须包含对TempPass的检查，并且仅当MVPD为NOT TempPass时才执行其逻辑。

- 的 `setAuthenticationStatus()` 和 `sendTrackingData()` 在身份验证完成后（与普通MVPD的无刷新流程完全相同）将调用回调。

>[!NOTE]
>
>此流仅可用于无刷新的TempPass。 对于刷新流，需要显式处理TempPass（当TempPass需要iFrame/弹出窗口时）

</br>

以下代码示例演示了如何在程序员网站上处理MVPD窗口（适用于普通MVPD和TempPass）：

```javascript
    var aeHostname = "https://entitlement.auth.adobe.com";
    var mvpdWindow = null;
    var mvpd = <mvpd_object_from_displayProviderDialog>;
    var useIframeLogin = <boolean_depending_on_browser_or_Programmer_preferences>;
    var backgroundLogin = <boolean_depending_on_Programmer_preferences>;
     
    // Do not create any windows for refreshless and temp pass
    if (!(backgroundLogin && mvpd.tempPass)) {
        if (backgroundLogin && !mvpd.popup) {
            mvpdWindow = window.open(aeHostname, "mvpdwindow");
        } else if (mvpd.popup && !useIframeLogin) {
            var width = mvpd.width;
            var height = mvpd.height;
            // Center on screen
            var top = (document.all) ? window.screenTop : window.screenY + 100;
            var left = (document.all) ? window.screenLeft : window.screenX + window.innerWidth / 2 - width / 2;
        
            mvpdWindow = window.open(aeHostname, "mvpdframe",
                           "width=" + width + ",height=" + height + ",top=" + top + ",left=" + left);
            // Monitor the mvpd popup for close
            if (!backgroundLogin) {
                clearInterval(cancelTimer);
                cancelTimer = setInterval(function () {
                    if (mvpdWindow && mvpdWindow.closed) {
                        clearInterval(cancelTimer);
                        $('#mvpddiv').hide();
                        accessEnablerAPI.setSelectedProvider(null);
                    }
                }, 200);
            }
        }
    }
```

