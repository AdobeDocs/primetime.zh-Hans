---
title: Primetime TVE Dashboard用户指南
description: Primetime TVE Dashboard用户指南
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '4386'
ht-degree: 0%

---


# Primetime TVE Dashboard用户指南 {#tve-db-user-guide}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## 简介 {#tve-db-intro}

[[!DNL Adobe] TVE功能板（TVE功能板）](https://console.auth.adobe.com/) 是一个自助功能板，面向为与Adobe Primetime身份验证产品团队有业务关系的媒体公司（程序员）工作的用户。

请联系您的技术客户经理(TAM)以获取访问权限。 要获取访问权限，您需要在Adobe Marketing Cloud组织中配置两个新用户组：

* TVE功能板读写 — 此组的成员对功能板的所有可编辑部分具有完全权限
* TVE功能板只读 — 此组的成员仅具有整个功能板的查看权限


在深入研究本用户指南之前，我们建议您先浏览以下资源，以便更好地了解Adobe Primetime身份验证产品团队提供的流程和功能，并熟悉本文档中使用的术语：

* [TVE技术文件](/help/authentication/technical-paper.md)
* [程序员Kickstart指南](/help/authentication/programmer-kickstart-guide.md)
* [授权流程](/help/authentication/entitlement-flow.md)
* [术语表](/help/authentication/glossary.md)


继续阅读本用户指南的下一部分，您将了解如何管理贵公司的渠道、节目制作人员或渠道与MVPD（多渠道视频节目分发商）之间的集成的不同设置。

>[!IMPORTANT]
>TVE功能板提供了在基本工作区和高级工作区之间切换的选项。 为此，您可以切换右上角的图标。 高级工作区面向具有丰富技术知识以及对Adobe Primetime身份验证产品团队所提供功能的高级知识的用户。

![TVE功能板工作区](assets/tve-basic-advanced-workspace.png)

*图1:Adobe Primetime TVE功能板“基本/高级工作区”下拉列表*

## 环境 {#authn-environments}

根据用户可能需要完成的任务，用户可能需要在Adobe Primetime身份验证环境之间进行切换。 有关Adobe Primetime身份验证环境的详细信息，请参阅以下文档： [了解Adobe Primetime身份验证环境](/help/authentication/understanding-the-adobe-environments.md).

TVE Dashboard提供了两个名为“预先鉴定”和“发布”的环境，每个环境都具有两个名为“暂存”和“生产”的配置文件，如下所示：

* [预定暂存](https://console-prequal.auth-staging.adobe.com/)
* [预准生产](https://console-prequal.auth.adobe.com/)
* [版本暂存](https://console.auth-staging.adobe.com/)
* [发行生产](https://console.auth.adobe.com/)

要在不同环境之间切换，用户可以单击如下所示下拉元素中的条目表示的所需环境：

![TVE功能板环境下拉列表](assets/tve-dashboard-env.png)

*图2:Adobe Primetime TVE功能板环境下拉列表*

>[!IMPORTANT]
>请务必注意，在通过TVE Dashboard对Adobe Primetime身份验证配置进行管理更改时，我们强烈建议您按照下面的顺序进行操作，以确保正确的功能。

要通过TVE功能板对Adobe Primetime身份验证配置进行管理更改，请执行以下操作：

* 在 [发行暂存环境并验证它们](http://sp.auth-staging.adobe.com/apitest/api.html).
* 在 [准备生产并验证它们](http://sp.auth-staging.adobe.com/apitest/api.html).
* 在 [发布生产并验证它们](http://sp.auth-staging.adobe.com/apitest/api.html).

>[!IMPORTANT]
>要使管理更改上线，用户必须通过选择将显示在侧栏左下角的按钮，导航到“查看和推送更改”部分，以便查看更改、添加新创建更改的描述，并通过选择“推送配置”确认配置更新。

![Tve功能板查看推送通知](assets/tve-review-push-notifications.png)

*图3:Adobe Primetime TVE功能板审阅和推送更改通知*

## 部分 {#sections}

为媒体公司（节目制作人）工作的用户可以从侧栏访问TVE仪表板的以下部分：

* **渠道**  — 包含与内容提供程序相关的设置
* **程序员**  — 包含与聚合一个或多个父组织相关的设置 **渠道**
* **集成**  — 包含与集成相关的设置 **渠道** 和 **MVPD**
* **MVPD**  — 包含与可用 **MVPD**
* **报表**  — 包含三种报表类型的汇总数据：AuthN TTL、AuthZ TTL、SSO
* **更改日志**  — 包含应用于TVE功能板配置的最新修改

![TVE功能板部分](assets/tve-dashboard-sections.png)

*图4:Adobe Primetime TVE功能板部分*

### 渠道 {#tve-db-channels-section}

利用此部分，可查看和编辑可用渠道的设置或创建新渠道的设置。 单击其中一个可用的渠道将返回一个包含以下选项卡的屏幕：

* **渠道数据**
   * **渠道ID**  — 我们系统中使用的渠道唯一ID，也称为“请求者ID”。
   * **显示名称**  — 渠道的商业名称。
* **常规设置**
   * **Analytics配置**  — 配置要转发到Adobe Primetime的Adobe Analytics身份验证事件。 有关在启用此功能之前需要如何配置报表包ID(RSID)的更多详细信息，请联系Adobe。
* **证书**

   包含验证流程中使用的证书列表及其发证组织、发证日期和到期日期。 这些证书将用作私钥/公钥，并用于验证。
* **域**

   包含相应渠道将与Adobe Primetime身份验证通信的域列表。
* **集成**

   包含与可用MVPD的集成列表，以及每个可能已启用或未启用的集成的状态。 通过单击特定条目，可导航到集成页面。
* **注册的应用程序**

   包含申请注册列表。 有关更多详细信息，请查看文档 [动态客户端注册管理](/help/authentication/dynamic-client-registration-management.md).

* **自定义方案**

   包含自定义方案列表。 有关更多详细信息，请参阅 [iOS/tvOS应用程序注册](/help/authentication/iostvos-application-registration.md) 和 [动态客户端注册管理](/help/authentication/dynamic-client-registration-management.md)


#### 添加/删除域 {#add-delete-domains}

要启动为所选渠道添加新域的过程，您需要单击域列表下方的“添加新域”按钮。 这将创建一个新的域条目，您可以在其中指定域名。 如果域列表中已存在更宽泛的域，则不应添加新的子域。

![向选定的渠道部分添加新域](assets/add-domain-to-channel-sec.png)

*图：渠道中的“域”选项卡*

### 程序员 {#tve-db-programmers-section}

此部分允许查看和编辑可用程序员的设置或创建新程序员的设置。 单击其中一个可用的程序员将返回一个包含以下选项卡的屏幕：

* **程序员数据**
   * **程序员Id**  — 程序员在我们系统中使用的唯一ID。
   * **显示名称**  — 程序员的商业名称。
   * **徽标Url**  — 程序员的商业徽标统一资源定位器(URL)。
   * **徽标预览**  — 从上述统一资源定位符(URL)下载程序员的商业徽标预览。

* **证书**

   包含验证流程中使用的证书列表及其发证组织、发证日期和到期日期。 这些证书将用作私钥/公钥，并用于验证。

* **渠道**

   包含属于此特定程序员的渠道列表。 通过单击特定条目，可导航到渠道部分。

* **注册的申请**

   包含申请注册列表。 有关更多详细信息，请参阅 [动态客户端注册管理](/help/authentication/dynamic-client-registration-management.md).

* **自定义方案**

   包含自定义方案列表。 有关更多详细信息，请参阅 [iOS/tvOS应用程序注册](/help/authentication/iostvos-application-registration.md) 和 [动态客户端注册管理](/help/authentication/dynamic-client-registration-management.md).


### 集成 {#tve-db-integrations-sec}

此部分允许查看和编辑渠道与可用MVPD之间的集成设置，或创建新的集成设置。 使用“基本工作区”时，单击其中一个可用的集成将返回一个页面；使用“高级工作区”时，单击带有以下选项卡的屏幕将返回一个页面：

* **集成数据**
   * **集成Id** — 将MVPD唯一ID附加到渠道的唯一ID中，并由“_”字符分隔。
   * **渠道显示名称**  — 渠道的商业名称。
   * **渠道ID**  — 我们系统中使用的渠道唯一ID，也称为“请求者ID”。
   * **MVPD显示名称** - MVPD的商业名称。
   * **MVPD Id**  — 在我们的系统中使用的MVPD的唯一ID。
* **常规设置**
   * **用户元数据键**  — 配置可用于特定集成的元数据键。
   * **平台特定设置**  — 为特定平台（例如，TTL、SSO和IFrame）配置不同的设置。

* **身份验证设置**
   * 包含与Adobe Primetime身份验证功能相关的设置。
* **授权设置**
   * 包含与Adobe Primetime身份验证授权功能相关的设置。
* **注销设置**
   * 包含与Adobe Primetime身份验证注销功能相关的设置。

#### 创建集成 {#create-integration}

要创建新集成，请执行以下步骤：

* 单击“添加新集成”按钮
* 搜索并选择渠道
* 搜索并选择MVPD
* 等待TVE功能板计算“集成ID”并显示可用的MVPD端点
* 选择身份验证、授权和注销端点或使用默认值
* 单击“创建集成”按钮
* 根据MVPD设置，可能会显示弹出窗口并要求获取其他属性（这些属性应该事先由MVPD提供），否则将发生到新创建的集成页面的重定向

![](assets/new-integration-window.png)



*图5. Adobe Primetime TVE功能板新集成窗口*


#### 更新集成 {#update-integration}

要更新现有集成，请从集成部分或渠道部分（包含集成选项卡）单击该特定集成的表条目。

使用基本工作区模式时，此部分将允许查看和编辑最常更新的设置，如身份验证和授权令牌TTL（存留期）以及iFrame设置。 请记住，与支持动态定义令牌持久性TTL的MVPD的集成可能缺少TTL设置(请参阅 [MVPD集成要求](/help/authentication/mvpd-integr-features.md))。



使用高级工作区模式时，此部分将允许查看和编辑不太常见的设置。



对于基本和高级工作区模式，可以在平台级别更改这些设置（例如，为Android上的授权TTL令牌选择自定义值，在其他平台上默认）。



>[!IMPORTANT]
>了解设置继承链非常重要：MVPD -> MVPD端点 — >集成 — >平台，其中平台具有最具体的值，而MVPD是最常用的默认值。

![](assets/inheritance-chain-component.png)


*图6. Adobe Primetime TVE功能板属性继承链组件*


#### 平台特定设置 {#platform-sp-settings}

此子部分可用于覆盖特定平台的设置。 可用平台包括：

* **所有平台**  — 设置将应用于所有平台的值，而不考虑程序员实施，以防没有为特定平台设置其他值。
* **Android**  — 设置将通过Adobe Primetime Authentication Android SDK应用于程序员实施的值。
* **无客户端REST API**  — 设置将通过Adobe Primetime Authentication REST API应用于程序员实施的值。
* **Fire TV**  — 设置值，这些值将应用于通过Adobe Primetime Authentication FireTV SDK进行的程序员实施。
* **FlashSDK**  — 此平台已弃用。 **已弃用**
* **JavaScript SDK**  — 设置将通过Adobe Primetime身份验证JavaScript SDK应用于程序员实施的值。
* **Roku**  — 设置将通过Adobe Primetime Authentication REST API应用于程序员实施的值，并将“Roku”作为设备类型发送。 对于Roku设备，此选项优先于为无客户端REST API平台设置的值。
* **Xbox本机SDK**  — 此平台已弃用。 **已弃用**
* **Xbox 360 REST API**  — 设置将通过Adobe Primetime Authentication REST API应用于程序员实施的值，并将“xbox”作为设备类型发送。 对于Xbox 360设备，这优先于为无客户端REST API平台设置的值。
* **Xbox One REST API**  — 设置将通过Adobe Primetime Authentication REST API应用于程序员实施的值，并将“xboxOne”作为设备类型发送。 对于XboxOne设备，此值优先于为无客户端REST Api平台设置的值。
* **iOS**  — 设置将通过Adobe Primetime Authentication iOS SDK应用于程序员实施的值。
* **tvOS**  — 设置将通过Adobe Primetime Authentication tvOS SDK应用于程序员实施的值。


![](assets/platform-sp-settings.png)

*图7. Adobe Primetime TVE仪表板平台特定设置*


#### 启用Platform单点登录 {#enable-platform-sso}

请按照以下步骤为特定集成和平台启用/禁用单点登录：

* 确保使用高级工作区模式
* 导航到所需的集成
* 导航到 **常规设置** 选项卡
* 选择要在其上启用或禁用单点登录的所需平台
* 切换 **启用单点登录** 标记为所需值（是/否）

   >[!IMPORTANT]
   >请务必注意， **启用单点登录** 标记仅适用于iOS、tvOS、Roku和FireTV平台，并且仅适用于与支持这些平台单点登录的MVPD集成。

* 切换 **强制平台权限** 标记为所需值（是/否）

   >[!IMPORTANT]
   >请务必注意， **强制平台权限** 标记控制用户是否将强制执行允许或拒绝平台访问其电视提供商订阅的决定。 在 **启用单点登录** 标志设置为“是”， **强制平台权限** 标记也设置为“是”，用户选择拒绝平台对其电视提供商订阅的访问，则相应的应用程序（渠道）将无法使用由其他应用程序（渠道）获取的Adobe Primetime身份验证令牌。


#### 启用基于家庭的身份验证 {#enable-hba}

请按照以下步骤启用/禁用 **OAuth2** 基于MVPD:

* 确保使用高级工作区模式
* 导航到所需的集成
* 导航到 **身份验证设置** 选项卡
* 导航到 **验证动态规则** 子选项卡
* 切换 **尝试HBA** 标记为所需值（是/否）


>[!IMPORTANT]
>请记住，“HBA AuthN TTL”值绝不应被覆盖，否则授权流可能会意外失败。

联系 **tve-support@adobe.com** 有关为基于SAML的MVPD启用主基身份验证的信息。

### MVPD {#tve-db-mvpds-sec}

此部分允许查看可用MVPD的设置。 单击其中一个可用的MVPD将返回一个带有以下选项卡的屏幕：

* **MVPD数据**
   * **MVPD Id**  — 在我们的系统中使用的MVPD的唯一ID。
   * **显示名称** - MVPD的商业名称，可在用户的选取器中使用。
   * **徽标Url** - MVPD的商业徽标统一资源定位器(URL)。
   * **徽标预览**  — 从上述统一资源定位符(URL)下载MVPD的商业徽标预览。
* **常规设置**
   * **用户元数据键**
      * 可用于特定MVPD的元数据键。
   * **客户端数据属性**
      * **身份验证/聚合器**  — 如果设置为“是”，则用户尝试访问的每个新渠道都需要新的身份验证令牌。
      * **已启用被动AuthN**  — 如果Auth / Aggregator标记设置为“是”，并且Passive AuthN Enabled设置为“是”，则后台将会进行其他渠道的身份验证过程，而无需完全浏览器重定向并显示选取器。
      * **身份验证/浏览器会话**  — 如果设置为“是”，则用户在关闭浏览器后将被注销。 如果设置为“否”，则用户可以重新启动浏览器并保持登录状态。
      * **IFrame必需**  — 如果设置为“是”，则表示MVPD登录窗口需要iFrame。 “iFrame Width”和“iFrame Height”字段表示加载MVPD登录页面所需的iFrame大小。
* **身份验证设置**
   * **选择端点**
      * 此字段表示MVPD公开的身份验证端点。 端点可能因所使用的身份验证协议而异。
   * **AuthN常规设置**
      * 此子选项卡显示MVPD使用的身份验证协议以及与协议相关的信息。
   * **AuthN证书**
      * 此子选项卡显示MVPD在身份验证流程中使用的证书及其颁发者组织、颁发日期和到期日期。 这些证书将用作私钥/公钥，并用于验证。
   * **验证动态规则**
      * 此子选项卡显示应用于身份验证过程的规则。 通过按图表的请求/响应/令牌，您可以看到高亮显示的参数，该参数应用于身份验证流程的该部分。
* **授权设置**
   * **选择端点**
      * 此字段表示MVPD公开的授权端点。 端点可能因所使用的授权协议而异。 可用的授权协议包括SOAP、REST（用于无客户端设备）、SAML、XACML和OAUTH。
   * **AuthZ常规设置**
      * 此子选项卡显示MVPD使用的授权协议和协议相关信息。
      * **预检配置**
         * 它描述了MVPD在单次呼叫中可预先授权的资源数、使用的PreFlight模型以及超时阈值。 有时，给定集成的资源数量可能会有所不同。 可通过编辑“**预检资源的最大数量**“常规设置”选项卡下的属性。 此属性仅适用于给定集成，如果设置，则将使用此属性，而不使用授权设置 — > PreFlight配置 — > PreFlight Max Resources中定义的值。
      * **DOS保护**
         * 它描述了MVPD授权端点上的拒绝服务保护。 有关每个字段的确切说明，请将鼠标悬停在DOS保护字段上以查看工具提示。
      * 如果MVPD是 **TempPass**，则 **AuthZ常规设置** 还包含有关TempPass持续时间的信息。
      * 如果MVPD是 **FlexibleTempPass**，则 **AuthZ常规设置** 还包含有关TempPass持续时间、最大资源数和标识字段的信息（请参阅下图）。
   * **AuthZ证书**
      * 此子选项卡显示MVPD在授权流程中使用的证书及其颁发者组织、颁发日期和到期日期。 这些证书将用作私钥/公钥，并用于验证。
   * **AuthZ动态规则**
      * 此子选项卡显示应用于授权流程的规则。 通过按图表 **请求/响应/令牌**，则可以查看高亮显示的应用于授权流程该部分的参数。
* **注销设置**
   * **选择端点**
      * 此字段指示MVPD公开的注销端点。 提供的协议可以是SAML或OAuth2。
      * **注销常规设置**
         * 此子选项卡显示MVPD使用的注销协议以及协议相关信息。
         * **要求注销响应已签名**  — 如果设置为“是”，则响应必须由受信任的证书签名。
      * **注销证书**
         * 此子选项卡显示MVPD在注销流程中使用的证书及其颁发者组织、颁发日期和到期日期。 这些证书将用作私钥/公钥，并用于验证。
      * **注销动态规则**
         * 此子选项卡显示适用于注销流程的规则。 通过按图表 **请求/响应/令牌**，则可以看到高亮显示应用于注销流程该部分的参数。

### 报表 {#tve-db-reports-sec}

要导航到此部分，请单击“[功能板部分](#sections)“ ”菜单。 这将导航到带有3个选项卡的屏幕，以下子部分将详细介绍该屏幕： [AuthN TTL报表](#authn-ttl-reports), [AuthZ TTL报表](#authz-ttl-reports), [单点登录报表](#sso-reports).

此部分允许查看和导出渠道与所有平台中各种MVPD集成的多种类型报表的汇总数据。

#### 平台 {#report-platforms}

所有报表都会在以下平台中聚合值：

**浏览器**
显示将通过Adobe Primetime身份验证JavaScript SDK应用于程序员实施的值。

**移动设备：iOS**
显示将通过Adobe Primetime Authentication iOS SDK应用于程序员实施的值。

**移动设备：ANDROID**
显示将通过Adobe Primetime Authentication Android SDK应用于程序员实施的值。

**移动设备：其他**
显示将应用于针对移动设备开发的通过Adobe Primetime Authentication REST API进行程序员实施的值。

**TVCD:ROKU**
显示将通过Adobe Primetime Authentication REST API应用于程序员实施的值，并将“Roku”作为设备类型发送。

**TVCD:FIRETV**
显示将通过Adobe Primetime Authentication FireTV SDK应用于程序员实施的值。

**TVCD:APPLETV**
显示将通过Adobe Primetime Authentication tvOS SDK应用于程序员实施的值。

**TVCD:其他**
显示将应用于针对电视连接设备开发的通过Adobe Primetime Authentication REST API的程序员实施的值。

**平台：未知**
显示将应用于程序员实施的值，Adobe Primetime身份验证服务会为其检测未知设备类型。

回顾 [传递客户端信息](/help/authentication/passing-client-information-device-connection-and-application.md) 到Adobe Primetime身份验证REST API或SDK，以了解有关如何发送所需设备类型（例如，“Roku”）的更多详细信息。

所有报表都基于每个Adobe Primetime身份验证环境的特定配置计算的聚合值。 因此，在不同的TVE功能板环境之间切换时，可能会得到不同的报表数据。

请查看 [环境](#authn-environments) 部分以了解与Adobe Primetime身份验证可用环境相关的更多详细信息。


##### 选择特定渠道/ MVPD {#selecting-specific-channels-mvpds}

所有报表都允许通过选择特定渠道或选择要包含在结果报表中的特定MVPD来使用过滤器。

要选择一个或多个渠道，请使用 **下拉列表** 放在“为报表选择的渠道”标签之后。 请参见图8。/9./10. 图像。

要选择一个或多个MVPD，请使用 **下拉列表** 放在“为报表选择的MVPD”标签之后。 请参见图8。/9./10. 图像。

默认情况下，数据会在贵公司的所有渠道（“所有渠道”）以及与之集成的MVPD（“所有MVPD”）之间进行聚合。

如果您选择取消选择“所有渠道”或“所有MVPD”而不选择特定选项，则UI将显示“无可用数据”占位符。


##### 导出报表 {#export-report}

所有报表都允许以逗号分隔值(CSV)格式文件导出数据。

要导出数据，请使用位于窗口右上角的“导出报表”按钮。 请参见图8。/9./10. 图像。

名为的文件 **Report.csv** 会自动下载到您的计算机。 因此，请确保您浏览器的设置允许下载文件。

计算Report.csv文件时，屏幕上将显示“导出数据”加载图标，该文件可能会 **几分钟** 根据要导出的数据大小。

#### AuthN TTL报表(#authn-ttl-reports)

此报表显示为渠道集成配置的验证令牌的生存时间(TTL)，该令牌在所有平台中具有各种MVPD。

身份验证令牌Time-To-Live，也称为 **AuthN TTL**，则会显示在人类可读的值中，例如： **天、小时、分钟、秒**.

根据用户体验，AuthN TTL报表允许您根据特定MVPD和特定平台，直观地检查用户将进行身份验证的时间。

要导航到此类型的报表，请单击“报表”部分中的“AuthN TTL报表”选项卡。

![AuthN TTL报表](assets/authn-ttl-reports.png)

*图8:Adobe Primetime TVE功能板身份验证TTL报表选项卡*

AuthN TTL报表表包含页面，并可水平和垂直滚动，具体取决于您的屏幕大小。

如果您考虑更改AuthN TTL值，请查看 [集成](#tve-db-integrations-sec) 中。

>[!IMPORTANT]
>“**由MVPD设置**&#x200B;当MVPD将是强制实施AuthN TTL值的MVPD，而不是Adobe Primetime身份验证配置时，会使用占位符。


#### AuthZ TTL报表 {#authz-ttl-reports}

此报表显示为您的渠道集成配置的授权令牌的生存时间(TTL)，该令牌在所有平台中具有各种MVPD。

授权令牌Time-To-Live，也称为 **AuthZ TTL**，则会显示在人类可读的值中，例如： **天、小时、分钟、秒**.

根据用户体验，AuthZ TTL报表允许您直观地检查用户在考虑特定MVPD和特定平台时获得授权的时间。

要导航到此类型的报表，请单击“报表”部分中的“AuthZ TTL报表”选项卡。

![AuthZ TTL报表](assets/authz-ttl-reports.png)

*图9. Adobe Primetime TVE功能板AuthZ TTL报表选项卡*

AuthZ TTL报表表包含页面，并可水平和垂直滚动，具体取决于您的屏幕大小。

如果您考虑更改AuthZ TTL值，请参阅 [集成](#tve-db-integrations-sec) 中。

>[!IMPORTANT]
>“**由MVPD设置**&#x200B;当MVPD将是强制实施AuthZ TTL值的MVPD，而不是Adobe Primetime身份验证配置时，会使用占位符。


#### 单点登录报表 {#sso-reports}

此报表显示为您的渠道集成配置的单点登录(SSO)状态，这些渠道与所有平台中的各种MVPD集成。

单点登录状态，也称为 **SSO状态**，将显示为具有以下可能值的三状态： **SSO已禁用， SSO已启用， SSO不确定**.

在用户体验方面，SSO报表允许您考虑特定MVPD和特定平台，以可视方式检查预期的用户身份验证SSO体验。

要导航到此类报表，请单击&#x200B;**单点登录报表**“ ”选项卡&#x200B;**报表**“ ”部分。


![TVE功能板单点登录报表选项卡](assets/sso-reports.png)


*图10:Adobe Primetime TVE功能板SSO报表选项卡*

SSO报表表包含页面，并且水平和垂直可滚动，具体取决于您的屏幕大小。

如果您考虑更改单点登录状态，请查看 [集成](#tve-db-integrations-sec) 中。

>[!IMPORTANT]
>&quot;**单点登录不确定**“在启用了SSO且可能启用SSO的情况下，会使用占位符，但用户平台设置/用户决策（例如，用户浏览器选项阻止第三方Cookie，用户选择拒绝平台访问其电视提供商订阅）或MVPD设置（例如，请求对每个渠道进行身份验证的MVPD）可能会阻止SSO的发生。

### 更改日志 {#tve-db-changelog-sec}

此部分显示通过TVE功能板推送到Adobe Primetime身份验证环境和配置的所有修改的列表。

有列可指示推送日期、操作修改的用户以及推送的状态。

此部分还允许比较两个表条目，以缩小您要检查的特定修改范围，甚至将比较作为邮件项目共享。

### 反馈 {#tve-db-feedback-sec}

此部分允许用户发送反馈。 按照以下步骤向Adobe Primetime身份验证产品团队提供反馈：

* 单击屏幕右侧的“Feedback”按钮
* 输入主题
* 输入消息
* 如果需要，可通过单击“上传屏幕截图”按钮，将屏幕截图上传到消息
* 单击“提交”按钮

![功能板反馈表](assets/tve-dashboard-feedback.png)

*图11:Adobe Primetime TVE功能板反馈部分*

有关如何捕获屏幕截图的说明，请查看以下链接：

* [如何在Windows上捕获屏幕截图](https://support.microsoft.com/en-us/windows/use-snipping-tool-to-capture-screenshots-00246869-1843-655f-f220-97299b865f6b#1TC=windows-7)

* [如何在Mac上捕获屏幕截图](https://support.apple.com/en-us/HT201361)

## 疑难解答 {#tve-db-troubleshoot}

### 维护模式 {#maintenance-mode}

![维护模式下的TVE应用](assets/tveapp-maintenance-mode.png)


*图：维护模式下的TVE应用*


如果TVE功能板处于“维护模式”，则用户将无法查看或进行新的更改。

如果发生这种情况，则需要等待Adobe Primetime认证工程团队在TVE仪表板上完成维护工作。

### 降级状态 {#degraded-state}

![TVE应用程序处于降级状态](assets/tve-degraded-state.png)


*图：TVE应用程序处于降级状态*

如果TVE功能板处于“降级”状态，则用户将缺乏搜索和排序功能，但用户将能够查看或进行新的更改。

如果发生这种情况，您将需要等待Adobe Primetime认证工程团队在TVE仪表板上完成维护工作。
