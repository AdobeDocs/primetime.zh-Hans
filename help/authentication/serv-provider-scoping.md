---
title: 服务提供商范围
description: 服务提供商范围
exl-id: 730c43e1-46c0-4eec-b562-b1ad93cce6d3
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# 服务提供商范围 {#service-provoider-scoping}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权的使用。

## 概述 {#overview}

Adobe Primetime身份验证与MVPD集成的默认实施基于 **OLCA规范**. OLCA规范的“身份验证要求”部分（6.5，主题标识符）规定，可以指明服务提供商(SP)的主题标识符的范围。 （主题标识符是MVPD返回到SP的经过模糊处理的用户ID。）  在Adobe Primetime身份验证集成中，要求MVPD启用SP身份验证请求的作用域。

由于Adobe Primetime身份验证扮演着SP的角色，程序员必须实施一种自定义设置，以便为身份验证请求设置SP范围。  此操作需要使MVPD能够识别在SAML断言中传递给MVPD的身份提供者(IdP)的网络品牌。  可以通过下一节中介绍的两种方式之一实施范围设定。

## 服务提供商范围 {#service-provider-scoping}

Adobe Primetime身份验证支持以下两种方式来启用身份验证请求的SP范围设定：

* **SAML发行者方法。**  在此方法中，“请求者ID”将附加到SAML身份验证请求中的SAML颁发者字符串。

* **自定义范围设置属性方法。**  在此方法中，“请求者ID”明确地作为自定义“Scoping”属性包含在SAML身份验证请求中。

>[!NOTE]
>
>“请求者ID”是Adobe Primetime身份验证如何指代程序员的网络品牌（例如：“CNN”是Turner网络的品牌之一）。

### SAML颁发者方法 {#saml-issuer-approach}

这种方法使用SAML `<Issuer>` 元素，如以下代码片段所示：

```xml
...
<saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">
    http://saml.sp.adobe.adobe.com/on-behalf-of/requestorID
</saml:Issuer>
...
```

### 自定义范围设置属性方法 {#custom-scoping-property-approach}

此方法使用名为“Scoping”的自定义属性，如SAML身份验证请求的以下代码片段中所示：

```xml
...
<samlp:Scoping xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <samlp:RequesterID xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">requestorID</samlp:RequesterID>
</samlp:Scoping>
...
```

<!--
>[!RELATEDINFORMATION]
>* [MVPD Authentication](/help/authentication/authn-usecase.md)
>* **OLCA Specification**
-->
