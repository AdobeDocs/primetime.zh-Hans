---
title: 服务提供商范围
description: 服务提供商范围
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---


# 服务提供商范围 {#service-provoider-scoping}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## 概述 {#overview}

与MVPD的Adobe Primetime身份验证集成的默认实施基于 **OLCA规范**. OLCA规范（6.5，主体标识符）的“身份验证要求”部分指出，可以为主体标识符指示服务提供商(SP)的范围。 （主题标识符是MVPD返回到SP的模糊处理用户ID。）  在Adobe Primetime身份验证集成中，需要MVPD启用SP身份验证请求的范围。

随着Adobe Primetime身份验证对程序员起到SP的作用，有必要实施一个自定义，以启用SP对身份验证请求的范围。  需要执行此操作，以便MVPD能够识别在SAML断言中传递到MVPD的标识提供程序(IdP)的网络品牌。  范围界定可以采用下一节中描述的两种方式之一来实施。

## 服务提供商范围 {#service-provider-scoping}

Adobe Primetime身份验证支持以下两种方法来启用身份验证请求的SP范围：

* **SAML颁发者方法。**  在此方法中，“请求者ID”将附加到SAML身份验证请求中的SAML颁发者字符串。

* **自定义范围属性方法。**  在此方法中，“请求者ID”明确作为自定义“范围”属性包含在SAML身份验证请求中。

>[!NOTE]
>
>“请求者ID”是Adobe Primetime身份验证指代程序员网络品牌的方式(例如：“CNN”是特纳网络的品牌之一。

### SAML颁发者方法 {#saml-issuer-approach}

此方法使用SAML `<Issuer>` 元素，如以下代码片段所示：

```xml
...
<saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">
    http://saml.sp.adobe.adobe.com/on-behalf-of/requestorID
</saml:Issuer>
...
```

### 自定义范围界定属性方法 {#custom-scoping-property-approach}

此方法使用名为“范围”的自定义属性，如SAML身份验证请求的此代码片段所示：

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