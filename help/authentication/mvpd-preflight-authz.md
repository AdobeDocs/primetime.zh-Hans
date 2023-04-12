---
title: MVPD预飞授权
description: MVPD预飞授权
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 0%

---


# MVPD预飞授权

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## 简介 {#mvpd-preflight-authz-intro}

“预检授权”是对多个资源的轻量级授权检查。 程序员主要使用它来装饰其UI（例如，通过锁定和解锁图标来指示访问状态）。

Adobe Primetime身份验证当前可以通过两种方式支持MVPD的预检授权，即通过AuthN响应属性或通过多通道AuthZ请求。  以下方案介绍了实施印前授权的不同方式的成本/收益：

* **最佳案例方案** - MVPD在授权阶段（多渠道AuthZ）提供预授权资源的列表。
* **最坏情况**  — 如果MVPD不支持任何形式的多资源授权，则Adobe Primetime身份验证服务器会为资源列表中的每个资源对MVPD执行授权调用。 此方案对飞行前授权请求的响应时间产生了影响（与资源数量成正比）。 它可能会增加Adobe和MVPD服务器上的负载，从而导致性能问题。 此外，它还将生成授权请求/响应事件，而无需实际播放。
* **已弃用** - MVPD在身份验证阶段提供预授权资源的列表，因此无需网络调用，甚至不需要预检请求，因为列表已缓存在客户端上。

虽然MVPD不必支持预飞授权，但以下各节介绍了Adobe Primetime身份验证可支持的一些预飞授权方法，然后才回退到上述最坏情况。

## AuthN中的预检 {#preflight-authn}

此预检方案为“OLCA兼容”(Cableabs)。 “身份验证和授权接口1.0规范”第7.5.2节标题为“身份验证断言中的属性语句”，描述SAML身份验证响应如何包含预授权资源列表。 如果IdP支持此功能，Adobe Primetime身份验证服务器将能够在身份验证时生成预先筛选的资源列表，并将其与身份验证令牌一起缓存在客户端上。 此方法还实现了最佳案例情景，当程序员调用checkPreauthorizedResources()时，不会执行网络调用，因为所有内容都在客户端上。

### SAML属性语句中的自定义资源列表 {#custom-res-saml-attr}

IdP的SAML身份验证响应应包含一个AttributeStatement，其中包含AdobePass应授权的资源名称。  某些MVPD会以下列格式提供此功能：

```XML
<saml:AttributeStatement>
  <saml:Attribute Name="authorized_resources">
    <saml:AttributeValue>MMOD</saml:AttributeValue>
    <saml:AttributeValue>Olympics2012</saml:AttributeValue>
  </saml:Attribute>
</saml:AttributeStatement>
```

以上示例显示包含两个预授权资源的列表：“MMOD”和“2012年奥运会”。

这有效地实现了最佳案例情景，并且当程序员调用checkPreauthorizedResources()时，不会执行网络调用，因为所有内容都在客户端上。

## AuthZ中的多通道预检 {#preflight-multich-authz}

此预检实施还兼容OLCA(Cablelabs)。  身份验证和授权接口1.0规范（第7.5.3和7.5.4节）描述了使用SAML断言或XACML从MVPD请求授权信息的方法。 在身份验证流程中，建议使用这种方法来查询不支持此功能的MVPD的授权状态。 Adobe Primetime身份验证向MVPD发出单次网络调用，以检索授权资源列表。


Adobe Primetime身份验证从程序员的应用程序接收资源列表。 Adobe Primetime身份验证的MVPD集成随后可以发起一个包含所有这些资源的AuthZ调用，然后解析响应并提取多个允许/拒绝决策。  使用多渠道AuthZ方案进行预检的流程如下所示：

1. 程序员的应用程序通过预检客户端API发送以逗号分隔的资源列表，例如：&quot;TestChannel1,TestChannel2,TestChannel3&quot;。
1. MVPD预检AuthZ请求调用包含多个资源，其结构如下：

```XML
<?xml version="1.0" encoding="UTF-8"?><soap11:Envelope xmlns:soap11="http://schemas.xmlsoap.org/soap/envelope/"> 
<soap11:Header/> 
<soap11:Body> 
  <xacml-samlp:XACMLAuthzDecisionQuery xmlns:xacml-samlp="urn:oasis:names:tc:xacml:2.0:profile:saml2.0:v2:schema:protocol" 
                                       CombinePolicies="false" Destination="https://login.idpexmaple.net/" ID="_3576604f382455d6495f342d9e07b69c" 
                                       IssueInstant="2013-02-07T10:31:40.333Z" Version="2.0"> 
  <saml2:Issuer xmlns:saml2="urn:oasis:names:tc:SAML:2.0:assertion">https://saml.sp.auth-staging.adobe.com/on-behalf-of/TestDistributors</saml2:Issuer> 
  <xacml-context:Request xmlns:xacml-context="urn:oasis:names:tc:xacml:2.0:context:schema:os"> 
  <xacml-context:Subject SubjectCategory="urn:oasis:names:tc:xacml:1.0:subject-category:access-subject"> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:subject:subject-id" DataType="http://www.w3.org/2001/XMLSchema#string"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
                                xsi:type="xacml-context:AttributeValueType">VFZTAQEAABQCe[...]</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Subject> 
  <xacml-context:Resource> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:resource:resource-id" DataType="http://www.w3.org/2001/XMLSchema#string"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
                                xsi:type="xacml-context:AttributeValueType">TestChannel1</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Resource> 
  <xacml-context:Resource> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:resource:resource-id" 
                           DataType="http://www.w3.org/2001/XMLSchema#string"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
                                xsi:type="xacml-context:AttributeValueType">TestChannel2</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Resource> 
  <xacml-context:Resource> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:resource:resource-id" 
                           DataType="http://www.w3.org/2001/XMLSchema#string"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                                xsi:type="xacml-context:AttributeValueType">TestChannel3</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Resource> 
  <xacml-context:Action> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:action:action-id" 
                           DataType="http://www.w3.org/2001/XMLSchema#string"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
                                xsi:type="xacml-context:AttributeValueType">VIEW</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Action> 
  <xacml-context:Environment> 
  <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:subject:authn-locality:ip-address" 
                           DataType="urn:oasis:names:tc:xacml:2.0:data-type:ipAddress"> 
  <xacml-context:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
                                xsi:type="xacml-context:AttributeValueType">127.0.0.1</xacml-context:AttributeValue> 
  </xacml-context:Attribute> 
  </xacml-context:Environment> 
  </xacml-context:Request> 
  </xacml-samlp:XACMLAuthzDecisionQuery> 
</soap11:Body> 
</soap11:Envelope>
```

## 多个资源的自定义授权 {#custom-authz}

某些MVPD在一个请求中具有支持对多个资源进行授权的授权端点，但它们不属于多渠道AuthZ中所述的情况。 这些特定的MVPD需要自定义工作。

Adobe还可以支持多渠道授权，而无需更改现有实施。  在Adobe和MVPD技术团队之间需要对此方法进行审核，以确保其能够按预期工作。

## 支持飞行前授权的MVPD {#mvpds-supp-preflight-authz}

下表列出了支持预检授权的MVPD，以及它们支持的预检类型和已知限制：

| 预飞法 | MVPD | 注释 |
|:-------------------------------:|:--------------------------------------------------------------------------------------------------------:|:------------------------------------------------------------------:|
| 多通道身份验证Z | Comcast AT&amp;T代理Clearleap Charter_Direct代理GLDS Rogers Verizon OSN Bell Sasktel Optimum AlticeOne |  |
| 用户元数据中的渠道阵容 | Suddenlink HTC | 所有Syncor直接集成也可以支持此方法。 |
| 分叉并连接 | 以上未列出的所有其他 | 选中的默认最大资源数= 5。 |

<!--
![RelatedInformation]
>* [Logout](/help/authentication/usecase-mvpd-logout.md)
>* [Authorization](/help/authentication/authz-usecase.md)
>* [MVPD Integration Features](/help/authentication/mvpd-integr-features.md)
>* [MVPD User Metadata Exchange](/help/authentication/mvpd-user-metadata-exchng.md)
>* [Preflight Authorization - Programmer Integration Guide](/help/authentication/preflight-authz.md)
>* [AuthN and AuthZ Interface 1.0 Specification](https://www.cablelabs.com/specifications/CL-SP-AUTH1.0-I04-120621.pdf){target=_blank} 
-->
