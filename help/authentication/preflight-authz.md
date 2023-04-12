---
title: 预检授权
description: 预检授权
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1512'
ht-degree: 0%

---



# 预检授权 {#preflight-authorization}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

</br>

## 概述 {#overview}

此功能为多个资源提供了轻量级的授权检查。 此轻量检查的目的是装饰UI（例如，使用锁图标和解锁图标指示访问状态）。 预检授权尽可能简单、高效，这样单个API调用就会生成资源列表的授权状态。 请注意，此功能在授权资源方面不具有权威性。

A `getAuthorization(resource)` 或 `checkAuthorization(resource)` 在允许播放之前，必须仍调用。

预检授权还为不同的用例提供支持，在该用例中，程序员需要请求对多个资源ID的授权，以便允许播放一项媒体内容。 程序员可以对所需资源进行初始预检，如果不满足业务条件，则根据响应情况，可能会提前失败。

有关支持飞行前授权的MVPD列表，请参阅 [MVPD预飞授权](/help/authentication/mvpd-preflight-authz.md#preflight_support_list) 页面。 

>[!NOTE]
>
> 请注意，对于没有完全飞行前授权支持的MVPD，需要预先与Adobe和MVPD商定使用此功能。 在这些MVPD上使用飞行前授权将属于描述的“最坏情况” [此处](/help/authentication/mvpd-preflight-authz.md#intro) 并且可能会导致性能问题和响应时间缓慢。 </br>
> 另外，请注意，使用 **需要由Adobe明确同意5个以上的资源**.

## AccessEnabler Preflight API {#AE_pre_api}

AccessEnabler公开了一个API/回调函数对来实施预检授权。 API调用采用一个参数，其中包含资源列表。 回调函数采用一个表示实际授权资源的参数。 以下示例已ActionScript，但AccessEnabler的所有版本都提供了这些调用。

### checkPreauthorizedResources(Array:resources):void {#checkPreauthRes}

在AccessEnabler对象上调用此函数，以请求资源列表的授权状态。

资源参数是应检查授权的资源列表。 列表中的每个元素都应是一个表示资源ID的字符串。 资源ID受与 `getAuthorization()` 呼叫，即在程序员与MVPD或媒体RSS片段之间建立的值上达成一致。 请注意，Adobe Primetime身份验证不会以任何方式管理资源，只是具有可以根据MVPD实际支持的内容来转换资源格式的精简中介层。

### preauthorizedResources(Array:authorizedResources) {#preauthRes}

这是一个回调函数，必须在程序员的上层应用程序中实现。 在计算授权资源列表后， AccessEnabler将调用此函数。


### JS示例

```javascript
    checkPreauthorizedResources(["CNBC","MSNBC"]);
    ...
    preauthorizedResources() {
        var resource = arguments[0];
        for(i in resources) {
            // Do things with resource list
            // such as decorate UI
            ...
        }
    }
```

## 实施信息 {#details}

- [使用ChannelID预检](#preflight_using_channelID)
- [POST/预授权](#post)
- [存储](#storage)

API调用会尝试在客户端的本地存储中查找当前用户的已授权资源的缓存列表。 如果没有缓存的列表，则会向AdobePass服务器发起HTTPS调用以检索该列表。

缓存机制通过完全跳过网络调用来缩短后续调用的性能时间。 此外，作为身份验证过程的一部分，还可以提前填充缓存列表。  (有关设置此方案的信息，请参阅 [预检授权集成](/help/authentication/authz-usecase.md#preflight_authz_int) （位于MVPD集成指南的授权部分）。

此外，缓存的资源列表可能用于优化授权流程，即如果存在缓存的资源列表， `checkAuthorization()` 可以在执行网络调用之前对其进行检查。 如果资源不在预授权资源列表中，则检查可能会失败，而无需调用Primetime身份验证服务器。


### 使用ChannelID预检 {#preflight_using_channelID}

从Primetime身份验证2.4.1版本开始，预检流程如下所示：

1. 在身份验证期间，Primetime身份验证会读取 `channelIID` 元素，并使用此值设置 `authorizedResources` 元素。
1. 内部 `checkPreauthorizedResources()` API函数，Primetime身份验证检查 `authorizedResources` 元素。
1. 如果 `authorizedResources` 元素，Primetime身份验证会读取该值，并从中执行资源列表之间的交集 `authorizedResources` 元素和从 `checkPreauthorizedResources()` 参数。  此交集的结果是预先授权的资源的最终列表。
1. 如果 `authorizedResources` 元素未设置，则执行先前实现的流程，其中接收自 `checkPreauthorizedResources()` 参数被传递到PreAuthorizationServlet。 此Servlet对MVPD端点执行授权调用并返回预授权资源列表。

### 使用ChannelID进行预检的示例

以下示例显示了一个示例渠道阵容。 请注意，用于将渠道列表发送到另一个MVPD的属性名称可能不同：

```XML
    <saml:Attribute Name="visible_channels" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
        <saml:AttributeValue xsi:type="xs:string">MSNBC</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">CNBC</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">FBN</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">FNC</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">TNT</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">TBS</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">CNN</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">TRUTV</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">TOON</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">HBO</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">MAX</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">EPIXHD</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">BTN-BTN2GO</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">SPEED-SPEED2</saml:AttributeValue>
    </saml:Attribute>
```
 

的 `authorizedResources` 身份验证元素中的元素如下所示：

```JSON
    <authorizedResources>
        <authorizedResource resourceID="MSNBC"/>
        <authorizedResource resourceID="CNBC"/>
        <authorizedResource resourceID="FBN"/>
        <authorizedResource resourceID="FNC"/>
        <authorizedResource resourceID="TNT"/>
        <authorizedResource resourceID="TBS"/>
        <authorizedResource resourceID="CNN"/>
        <authorizedResource resourceID="TRUTV"/>
        <authorizedResource resourceID="TOON"/>
        <authorizedResource resourceID="HBO"/>
        <authorizedResource resourceID="MAX"/>
        <authorizedResource resourceID="EPIXHD"/>
        <authorizedResource resourceID="BTN-BTN2GO"/>
        <authorizedResource resourceID="SPEED-SPEED2"/>
    </authorizedResources>
```

程序员执行 `checkPreauthorizedResources()` API调用，以传递以下参数列表：</span>

- &quot;MSNBC&quot; 
- &quot;FBN&quot; 
- &quot;TruTV&quot;
- &quot;fbc-fox&quot;

当前的Preflight实施执行与 `authorizedResources` 元素，并返回此列表：

- &quot;MSNBC&quot;
- &quot;FBN&quot;
- &quot;TruTV&quot;

 

**注意：** 请注意，交集不区分大小写。

 

### POST/预授权 {#post}

当不存在缓存、授权、资源列表时，AccessEnabler将自动执行此调用。 


#### 请求 {#req}

| 参数 | 类型 | 必需 | 描述 |
| --- | --- | --- | --- |
| `authentication_token` | 字符串 | 是 | 身份验证令牌。 |
| `resource_id` | 字符串 | 是 | 单个资源。 可以多次指定此值，在 `checkPreauthorizedResources()` API调用。 |


**注意：** 可以配置请求的最大资源数。
**最大默认值为5。**


#### 响应 {#resp}

预授权Servlet发回的响应格式如下：

```XML
    <?xml version="1.0" encoding="UTF-8"?>
    <resources>
      <resource>
        <id>TNT</id>
        <authorized>true</authorized>
      </resource>
      <resource>
        <id>TBS</id>
        <authorized>true</authorized>
      </resource>
      <resource>
        <id>CNN</id>
        <authorized>false</authorized>
      </resource>
    </resources>
```

### 存储 {#storage}

AccessEnabler从服务提供商获取的预授权资源列表。 以下资源列表：

- 与AuthN和AuthZ令牌一起存储
- 只要用户位于同一网站上，或者在AuthN令牌过期之前有效
- 每当用户登陆新的Primetime身份验证集成网站时，便会重新检索该网站

每个条目都包含用户预先授权的资源ID。

例如：


| 资源ID | 已授权 |
| ----------- | ---------- |
| CNN | true |
| TNT | false |
| ... | ... |


此列表名为“预授权缓存”。

#### 流量 {#flow}

1. 程序员应用程序/网站将 `checkPreauthorizedResources(resourceList)` 呼叫。
1. AccessEnabler验证授权资源的身份验证令牌：
   1. 如果身份验证令牌包含授权资源 — 此列表是授权的，则不应进行任何调用以获取此信息。 在身份验证令牌上的授权资源列表内搜索resourceList中的资源，并且只返回那些已找到的资源 `preauthorizedResources()` 回调。
   1. 如果身份验证令牌不包含授权资源 —  `resourceList` 与预授权缓存中的资源列表进行比较。
      1. 如果列表包含相同的资源 — 这表示已对服务器进行调用，并且响应已位于预授权缓存中。 只有获得授权的资源才会由 `preauthorizedResources()` 回调。
      1. 如果列表DOES NOT包含相同的资源，则客户端需要对服务器进行调用，以获取resourceList中资源的授权状态。 将获取响应并将其存储在预授权缓存中，以完全替换旧资源。 只有获得授权的资源才会由 `preauthorizedResources()` 回调。


#### 列表检索 {#listRetrieve}

只要 `checkPreauthorizedResources()` 调用时，将针对预授权缓存检查要验证授权的资源列表。 如果列表包含相同的资源集，则不会调用服务提供商，因为触发 `preauthorizedResources()` 回调已在缓存中。


#### logout() {#logout}

注销时会清空预授权缓存。


## 依赖关系 {#depends}

预检API的性能取决于特定的MVPD实施。  有关实施选项，请参阅 [预检授权集成](/help/authentication/authz-usecase.md#preflight_authz_int) （位于MVPD集成指南的授权部分）。


## 安全性 {#security}

客户端API可供所有程序员使用。

该实施使用HTTPS作为传输，但为了进行更轻松的调用，不会使用其他安全措施（无签名、无FAXS）。

**注意：** 请勿以权威方式使用此API来确定是否应向用户授予对受保护资源的访问权限。 此API的用途是进行UI修饰和/或预先制定业务决策。 的 `getAuthorization()` 和 `checkAuthorization()` 应始终在允许播放之前发起调用。


## 兼容性 {#compat}

AccessEnabler的所有版本都支持此功能：AS、JS、AIR、iOS、Android、Xbox（在第2屏幕AuthN流程中）。

预授权不支持包含CDATA节的预授权资源。 目前飞行前系统的重点是支持信道级滤波。 包含CDATA部分的资源可能是资产级别的资源。 预检功能支持简单 `mrss` 渠道级别预授权的资源，只要它们不包含CDATA。 

## 与其他功能集成 {#integ_w_other_features}

如果资源不在预授权资源列表中，则可能的优化可在授权流上发生，以便快速失败。

在此优化中，服务器预检终结点与降级机制集成。  

如果MVPD和请求者已设置“AuthN All”规则，则预检端点将只镜像请求中接收的所有资源。

如果为请求中存在的至少一个资源启用了“AuthZ All”，则情况也是如此。

<!--
## Related Information

  - `checkPreauthorizedResources()`
      - [iOS](#checkPreauth)
      - [Android](#checkPreauth)
      - [JavaScript](#checkPreauthRes)
      - [ActionScript](#checkPreauthRes)
  - [Xbox](#2nd%20Screen%20Authentication)
  - [MVPD Integration Guide: Preflight AuthZ](#)
-->
