---
title: Safari浏览器的JS SDK限制
description: Safari浏览器的JS SDK限制
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1804'
ht-degree: 0%

---

# Safari浏览器的JS SDK限制 {#js-sdk-limitations-for-safari-browser}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

<!--
>[!IMPORTANT] 
>
>We are strongly recommending [migration to AccessEnabler JavaScript SDK versions 4.x](http://tve.helpdocsonline.com/accessenabler-js-v4-migration-guide) in order to have a stable and predictable behavior on Safari browser.-->


## Safari 10 {#safari10}

**详细信息**

* 从Safari 10开始，默认的浏览器隐私设置将导致单点登录(SSO)、单次注销(SLO)和被动身份验证功能停止工作。 即使在多个选项卡或浏览器窗口之间的同一会话中，单点登录(SSO)和被动身份验证也无法正常工作。

* 这些更改会对以下版本的AccessEnabler JavaScript SDK的Adobe Primetime身份验证流程造成影响，并正在产生影响：v2（版本2.x）、v3（版本3.x）、v4（版本4.x）。

### 缓解 {#mitigation-safari10}

* 为了缓解这些限制，您可以指示用户更改Safari 10浏览器的隐私设置，并使用“**始终允许**“ ”选项&#x200B;**Cookie和网站数据**“ ”(在浏览器的“隐私”选项卡的“首选项”中输入，如下图所示。

   ![](assets/always-allow-safari10.png)


## Safari 11 {#safari11}

**详细信息**

>[!IMPORTANT]
>
>对于Safari 11,Safari 10部分中的所有上述详细信息仍适用。

* 从Safari 11开始，浏览器引入 [智能防跟踪](https://webkit.org/blog/7675/intelligent-tracking-prevention/)(ITP)机制，一种使用启发式技术来防止跨站点跟踪的技术。 这些启发式方法会影响在网络调用中存储和重播第三方Cookie的方式，这意味着根据ITP机制激活，Safari浏览器将阻止客户端 — 服务器模型通信中的第三方Cookie。

* Adobe Primetime身份验证服务在身份验证过程中使用并依赖Cookie **以便发挥作用**. 如果身份验证过程自动进行（例如临时通过），或者在使用iFrame或“无刷”功能的实施中，Adobe的Cookie会被视为第三方Cookie，并且默认情况下会被阻止。 对于任何其他情况，Safari会使用机器学习算法，该算法可能会将所有Adobe的Primetime身份验证服务Cookie标记为跟踪Cookie，因此受ITP阻止的约束。  

* 总之，激活智能防跟踪(ITP)机制后，Safari 11浏览器的用户可能无法在启用Adobe Primetime身份验证的网站上进行身份验证，尤其是当用户使用多个启用Adobe优先级身份验证的网站时。 因此，用户的身份验证体验可能会出现意外且未定义，从无法登录到比预期的身份验证持续时间更短。

* 这些更改会影响以下版本的AccessEnabler JavaScript SDK的Adobe Primetime身份验证流程，并会对其产生影响：v2（版本2.x）、v3（版本3.x）。

### 缓解 {#mitigation-safari11}

* 对于AccessEnabler JavaScript SDK v3（版本3.x）和AccessEnabler JavaScript SDK v4（版本4.x），库包含一种机制，可识别由于缺少所需Cookie而阻止用户身份验证的情况。 在这些情况下，库会触发特定错误回调 [N130](/help/authentication/error-reporting.md#advanced-error-codes-reference)，可传递回已启用Adobe Primetime身份验证的网站，以用作指示用户采取可缓解问题的操作的信号。 为了从这一机制中受益，网站必须实施 [错误报告](/help/authentication/error-reporting.md) 规范。

* 对于AccessEnabler JavaScript SDK v2（版本2.x），库不提供上述机制，因此在指示用户采取措施以缓解问题时，无法向启用了Adobe Primetime身份验证的网站发出信号。

* 可减轻上述问题的行动清单 **适用于所有三个版本** AccessEnabler JavaScript SDK的ID。

* When [N130](/help/authentication/error-reporting.md#advanced-error-codes-reference) 实施者的网站收到错误回调，应指示用户禁用智能防跟踪(ITP)并通过以下方式启用第三方Cookie:

* 对于Mac OS X High Sierra及更高版本：正在取消选中“**防止跨站点跟踪**“ ”选项&#x200B;**网站跟踪**“ ”(在浏览器的“隐私”选项卡的“首选项”中输入，如下图所示。

   ![](assets/uncheck-prvnt-cr-st-tr-safari11.png)

* 对于Mac OS X Sierra和之前版本：正在检查“**始终允许**“ ”选项&#x200B;**Cookie和网站数据**“ ”(在浏览器的“隐私”选项卡的“首选项”中输入，如下图所示。

   ![](assets/always-allow-safari11.png)

## Safari 12 {#safari12}

**详细信息**

>[!IMPORTANT]
>
>对于Safari 12,Safari 10部分和Safari 11部分中的所有上述详细信息仍适用。

本节详细介绍 **AccessEnabler JavaScript SDK版本4.x** 在Safari 12上。

>[!NOTE]
>
>请记住，对于AccessEnabler JavaScript SDK版本2.x和AccessEnabler JavaScript SDK版本3.x，它们都使用第三方Cookie进行身份验证过程，并且由于从Safari 11开始的ITP和第三方Cookie策略，用户的身份验证体验可能会意外且未定义，从无法登录到比预期的身份验证持续时间更短。


### Safari 12上AccessEnabler JavaScript SDK v4（版本4.x）的认证功能 {#certified-functionality-of-accessenabler-javacscript=sdk-v4}

* **身份验证** 即使用户的浏览器禁用了第三方Cookie，利用用户交互的流也将始终有效，因为从版本4.0开始，AccessEnabler JavaScript SDK不再将第三方Cookie用于身份验证过程。

>[!NOTE]
>
>用户必须与站点进行交互，才能打开登录弹出窗口和/或与MVPD登录页面进行交互。

* **授权/预检/用户元数据** 如果用户已经进行了身份验证，则操作会完全正常运行。

### Safari 12上的AccessEnabler JavaScript SDK v4（版本4.x）的已知问题 {#known-issues-of-accessenabler-javascript-sdk-4}

* 单点登录和单点登录

   * 由于从Safari 10开始在Safari中实施localStorage的方式，JS SDK无法再通过通用域iFrame共享登录状态。 这意味着用户需要登录使用AccessEnabler JavaScript SDK的每个站点。 注销也不会删除跨站点的身份验证令牌，因此用户需要从每个启用了Adobe Primetime身份验证的网站中注销。

* 临时通道

   * 对于临时传递，AccessEnabler JavaScript SDK使用个性化机制，以便将身份验证令牌锁定到特定设备（浏览器实例）。 由于Safari 12中设计了新机制来阻止跟踪，我们正在计算并在个性化机制中使用指纹 **对于具有相同IP地址的所有用户，将是相同的**. 出于个性化目的，我们确实考虑了客户端IP，但即便如此，这也会对共享相同公共IP地址的用户产生影响。 对于这些用户，我们将计算相同的个性化ID，并将临时传递绑定到该ID。 这意味着，一旦此类用户使用临时通行证，其他用户将无权访问\! 这会对使用NAT或公共代理访问互联网的多个用户的企业用户、教育机构或任何其他组织产生特别的影响。

>[!NOTE]
>
>仅当实施者因用户交互而使用临时传递时，此问题才会影响用户，否则，临时传递身份验证受 **自动流量** 下。

* 自动流量

   * 使用JS SDK 4.0时，在自动模式下尝试的身份验证流程在Safari 12中不会成功，且没有任何用户交互。请注意，即将推出的JS SDK 4.1修复了自动流程的所有问题。

受此问题影响的用例：

* 自动TempPass（免费预览）身份验证 — 对于此类流，SDK将引发N130错误。

* 被动身份验证（无提示失败） — 要求用户选择此MVPD并输入凭据

### 缓解 {#mitigation-safari12}

**单点登录和单点登录**

在编写本文时，没有已知的缓解措施可用或可能。 Apple确实在Safari 12中引入了“存储访问API”(`https://webkit.org/blog/8124/introducing-storage-access-api`)，但当前实施不适用于localStorage，而仅适用于cookie。 此外，API要求用户进行交互才能使用，一旦您使用，系统也会在提示用户时显示与下面类似的权限对话框。

![](assets/permission-dialog-apple.png)


此时，这些Safari要求/提示与我们的UX要求不一致，而且我们的行为与其他浏览器不一致，在其他浏览器中，当我们将令牌保存到通用域localStorage中后，单点登录(SSO)即“正常工作”。

**临时通道**

为了缓解个性化问题并进行用户交互，我们建议您使用 **[提升临时通行证 ](/help/authentication/promotional-temp-pass.md)** 以交互方式，并提供至少一个关于用户的附加信息（例如，电子邮件地址）。

## Safari 13 {#safari13}

**详细信息**

>[!IMPORTANT]
>
>从Safari 10部分到Safari 12部分的所有上述详细信息在Safari 13的情况下仍适用。


从Safari 13开始，浏览器对 [智能防跟踪](https://webkit.org/blog/7675/intelligent-tracking-prevention/) (ITP)，从而在将第三方Cookie标记为跟踪Cookie的过程中更加严格地实施机制背后的启发式算法，以防止跨站点跟踪。

如前几节所述，当实施者使用AccessEnabler JavaScript SDK v2（版本2.x）和AccessEnabler JavaScript SDK v3（版本3.x）时，Adobe Primetime身份验证服务会使用并依赖第三方Cookie作为身份验证流程的一部分。 与Safari浏览器的先前版本相比，当ITP花费一段时间以“了解”用户与参与方(程序员网站和Adobe)之间的交互时，Safari 13浏览器会阻止第三方Cookie（在客户端 — 服务器模型通信中被视为跟踪Cookie）的开始。

总之，Safari 13浏览器的用户很可能无法在启用了Adobe Primetime Authentication的网站上启动新身份验证，该网站使用的是旧版AccessEnabler JavaScript SDK、v2（版本2.x）或v3（版本3.x）。 之所以会出现这种情况，是因为ITP阻止了所有必需Adobe的Primetime身份验证服务Cookie，从而导致该服务无法满足身份验证请求。

AccessEnabler JavaScript SDK v4（版本4.x）库不使用第三方Cookie进行身份验证过程，因此其操作不会因Safari 13更改而受到任何影响。

### 缓解 {#mitigation-safari13}

我们首先强烈建议 **迁移到AccessEnabler JavaScript SDK版本4.x** 以在Safari浏览器上实现稳定且可预测的行为。

其次，对于AccessEnabler JavaScript SDK v3（版本3.x），库包含一种机制，可识别由于缺少所需的Cookie而阻止用户身份验证的情况。 在这些情况下，库会触发特定错误回调([N130](/help/authentication/error-reporting.md#advanced-error-codes-reference))，该ID将传递回已启用Adobe Primetime身份验证的网站，以用作指示用户采取可缓解问题的操作的信号。 为了从这一机制中受益，网站必须实施 [错误报告](/help/authentication/error-reporting.md) 规范。

对于AccessEnabler JavaScript SDK v2（版本2.x），库不提供上述机制，因此在指示用户采取措施以缓解问题时，无法向启用了Adobe Primetime身份验证的网站发出信号。

When [N130](/help/authentication/error-reporting.md#advanced-error-codes-reference) 实施者的网站收到错误回调，应指示用户禁用智能防跟踪(ITP)并通过以下方式启用第三方Cookie:

* 对于Mac OS X High Sierra及更高版本：正在取消选中“**防止跨站点跟踪**“ ”选项&#x200B;**网站跟踪**“ ”(在浏览器的“隐私”选项卡的“首选项”中输入，如下图所示。

   ![](assets/prvnt-cross-site-tr-safari13.png)

* 对于Mac OS X Sierra和之前版本：检查t</span>he &quot;**始终允许**“ ”选项&#x200B;**Cookie和网站数据**“ ”(在浏览器的“隐私”选项卡的“首选项”中输入，如下图所示。

   ![](assets/always-allow-safari13.png)

