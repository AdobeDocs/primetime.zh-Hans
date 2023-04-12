---
title: MVPD授权
description: MVPD授权
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---


# MVPD授权

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## 概述 {#mvpd-authz-overview}

授权(AuthZ)是通过Adobe托管的后端服务器与MVPD AuthZ端点之间的后通道（服务器到服务器）通信来执行的。

对于AuthZ请求，授权端点应至少能够处理以下参数：

* **Uid**. 从身份验证步骤接收的用户ID。

* **资源ID**. 标识给定内容资源的字符串。 此资源ID由程序员指定，MVPD必须加强这些资源上的业务规则（例如，检查用户是否订阅了特定渠道）。

除了确定用户是否已授权外，响应还必须包含此授权的生存时间(TTL)，即授权过期时。 如果未设置TTL，则AuthZ请求将失败。  因此， **TTL是Adobe Primetime身份验证端的强制配置设置**，以覆盖MVPD在其请求中不包含TTL的情况。

## 授权请求 {#authz-req}

AuthZ请求必须包括代表其发出请求的主题、主题尝试访问的资源、主题尝试对资源执行的操作以及将要进行操作的环境。 在Adobe Primetime身份验证的特定情况下，这些元素对应于：

| XACML元素 | 对应于 |
|---------------|--------------------------------------------------------------------------------------------------------------------------------|
| 主题 | 由已验证会话标识的主体，由SAML断言的“主题令牌”属性值引用。 |
| 资源 | 受保护资源的URI。 |
| 操作 | 查看。 |
| 环境 | 包括请求客户端的IP地址，如SP所见。 |



此时，SP必须准备XACML授权DecisionQuery，并(通过HTTPPOST)将其发送到（先前商定的）策略决策点(PDP)以获取IdP。 以下是简单XACML请求的示例（请参阅XACML核心规范）：

```XML
POST https://authz.site.com/XACML_endpoint
<Request  xmlns="urn:oasis:names:tc:xacm:2.0:context:schema:os"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="urn:oasis:names:tc:xacml:2.0:context:schema:os
http://docs.oasis-open.org/xacml/access_control-xacml-2.0-context-schema-os.xsd">
<Subject>
   <Attribute
        AttributeId="urn:oasis:names:tc:xacml:1.0:subject:subject-token"
        DataType="http://www.w3.org/2001/XMLSchema#base64Binary">
      <AttributeValue>{Base64 Data}</AttributeValue>
   </Attribute>
</Subject>
<Resource>
   <Attribute
        AttributeId="urn:oasis:names:tc:xacml:1.0:resource:resource-id"
        DataType="http://www.w3.org/2001/XMLSchema#anyURI">
<AttributeValue>urn:tve:tms:1234</AttributeValue>
   </Attribute>
</Resource>
<Action>
   <Attribute
        AttributeId="urn:oasis:names:tc:xacml:1.0:action:action-id"
        DataType="http://www.w3.org/2001/XMLSchema#string">
       <AttributeValue>VIEW</AttributeValue>
   </Attribute>
</Action>
<Environment>
   <Attribute
       AttributeId="urn:oasis:names:tc:xacml:1.0:subject:authn-locality:ip-address"
       DataType="http://www.w3.org/2001/XMLSchema#string">
      <AttributeValue>1.2.3.4</AttributeValue>
   </Attribute>
</Environment>
</Request>
```


在收到AuthZ请求后，MVPD的PDP会评估该请求，并确定是否应允许主题对资源执行所请求的操作。 然后，MVPD会返回包含决策、状态代码和消息的响应，如下面的授权响应中所述。

## 授权响应 {#authz-response}

在MVPD评估请求并应用所请求的业务规则以确定是否允许主体对资源执行所请求的操作之后，才会响应AuthZ请求。 返回的对Adobe Primetime身份验证的响应在XACML核心规范之后再次表示，该规范包含SP作为策略执行点(PEP)的决策、状态代码、消息和义务。 以下是一个示例响应：

```XML
<Response xmlns="urn:oasis:names:tc:xacml:2.0:context:schema:os">
  <Result>
  <Decision>Permit</Decision>
  <Status>
     <StatusCode Value="urn:oasis:names:tc:xacml:1.0:status:ok"/>
     <StatusMessage>ok</StatusMessage>
  </Status>
  <xacml:Obligations     
          xmlns:xacml="urn:oasis:names:tc:xacml:2.0:policy:schema:os">
     <xacml:Obligation    
              ObligationId="urn:cablelabs:olca:1.0:obligations:log"
              FulfillOn="Permit" />
  </xacml:Obligations>
 </Result>
</Response>
```

以下是Adobe Primetime身份验证支持并使程序员能够履行的DENY义务列表：

* **urn:tve:xacml:2.0:obligations:restrict-pc**  — 订阅者未通过家长控制检查，SP必须采取适当措施限制对此内容的访问。

* **urn:tve:xacml:2.0:obligations:升级**  — 订阅者没有适当的订阅级别。  必须升级订阅才能访问内容。

Adobe Primetime身份验证支持以下 **许可** 程序员可履行义务，并使其能够履行这些义务：

* **urn:cablelabs:olca:1.0:obligations:日志** -Adobe Pass记录交易，并可通过商定的报告机制提供。

* **urn:cablelabs:olca:1.0:obligations:re-authz** - Adobe Primetime身份验证会在n秒内再次刷新授权（通过XACML AttributeAssignment指定为Odivity的参数 — 请参阅XACML核心规范第5.46节）。

<!--
>![RelatedInformation]
>* [Preflight Authorization](/help/authentication/preflight-authz.md)
>* [Authentication](/help/authentication/authn-usecase.md)
-->