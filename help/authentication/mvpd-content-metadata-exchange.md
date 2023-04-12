---
title: MVPD内容元数据交换
description: MVPD内容元数据交换
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---


# MVPD内容元数据交换

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## 概述 {#content-metadat-exchange-overview}

本页介绍了Adobe Primetime身份验证用于在授权请求中将结构化数据发送到MVPD的两种标准实施。  结构化数据表示提出请求的资源（程序员），并且可能还表示其他数据，如内容评级。

在程序员方面，Adobe Primetime身份验证支持结构化的MRSS数据资源，如下所示：

1. 程序员将资源作为MRSS字符串发送。 Adobe Primetime身份验证不会在客户端为web设备或本机设备进行编码。 MRSS将作为常规字符串发送到Adobe Primetime身份验证服务器。
1. 在服务器端，将根据预定义的架构(http://search.yahoo.com/mrss/)验证MRSS。  如果验证通过，Adobe Primetime身份验证会从MRSS字段中提取信息，包括：
   * 频道标题
   * 项目标题
   * 资源标识符
   * 评级值和类型
1. 从MRSS提取的值用于构建将传递到MVPD的授权请求。

Adobe Primetime身份验证支持两种将MRSS转换为MVPD支持的格式的方法：

* **XACML**.  第一种方法与OLCA标准一致。  它使用XACML，其中会提取MRSS值，以使用映射到MRSS元素的属性来构建XACMLResource。  然后，该数据会传递到MVPD。
* **REST**.  第二种方法是基于REST。  MRSS是base64编码，在REST调用中作为URL参数传递。

在这两种方法中，MVPD通过将提取的值包含在其自身的逻辑流中并返回授权响应来处理授权请求。

## 集成详细信息 {#integration-details}

* 基于OLCA的XACML结构化资源
* 基于REST的结构化资源

### 基于OLCA的XACML结构化资源 {#olca-based-xacml-struc-resource}

大多数面向电缆的MVPD都使用基于XACML的方法，但尚不支持完整的结构化数据方法。  其他支持XACML的MVPD将采用渠道标题，并接受该标题作为ResourceID属性。 以下示例显示了基于XACML的完整结构化方法。 Adobe Primetime身份验证团队建议，对于使用XACML但尚不支持家长控制等功能的MVPD，他们应当将其XACML集成调整为以下示例：

```XML
<?xml version="1.0" encoding="UTF-8"?>
<soap11:Envelope xmlns:soap11=">
    <soap11:Header/>
    <soap11:Body>
        <xacml-samlp:XACMLAuthzDecisionQuery
                xmlns:xacml-samlp="urn:oasis:names:tc:xacml:2.0:profile:saml2.0:v2:schema:protocol"
                Destination="
                ID="_f1dd34469c5aeac016760e51dbba007d" IssueInstant="2012-06-26T16:30:24.879Z" Version="2.0">
            <saml:Issuer xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion">
                https://saml.sp.auth.adobe.com/
            </saml:Issuer>
            <ds:Signature xmlns:ds=">.......</ds:Signature>
            <xacml-context:Request xmlns:xacml-context="urn:oasis:names:tc:xacml:2.0:context:schema:os">
                [....info skipped for brevity....]
                <xacml-context:Resource>
 
        // The MRSS item GUID is passed as the XACML Resource resource-id
                    <xacml-context:Attribute AttributeId="urn:oasis:names:tc:xacml:1.0:resource:resource-id">
                        <xacml-context:AttributeValue>DISNEY_GUID_12345</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
        // The MRSS channel title is passed as the XACML Resource tv-network
                    <xacml-context:Attribute AttributeId="urn:cablelabs:ocla:1.0:attribute:content:tv-network">
                        <xacml-context:AttributeValue>Disney</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
 
        // Adobe doesn't yet support an explicit namespace for the GUID, so we reuse the channel title as the GUID.  
        // We expect to add an explicit namespace later next year pulling it from the GUID scheme attribute.
                    <xacml-context:Attribute AttributeId="urn:cablelabs:ocla:1.0:attribute:content:id:namespace">
                        <xacml-context:AttributeValue>Disney</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
 
        // The MRSS item title is passed as the XACML Resource content title
                    <xacml-context:Attribute AttributeId="urn:cablelabs:ocla:1.0:attribute:content:title">
                        <xacml-context:AttributeValue>Disney Program X</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
 
        // The MRSS media rating is passed as the XACML Resource content rating 
                    <xacml-context:Attribute AttributeId="urn:cablelabs:ocla:1.0:attribute:content:rating:vchip">
                        <xacml-context:AttributeValue>TV-Y</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
 
                </xacml-context:Resource>
 
                <xacml-context:Action>
                    <xacml-context:Attribute>
                        <xacml-context:AttributeValue>VIEW</xacml-context:AttributeValue>
                    </xacml-context:Attribute>
                </xacml-context:Action>
 
                [.....info skipped for brevity....]
            </xacml-context:Request>
        </xacml-samlp:XACMLAuthzDecisionQuery>
    </soap11:Body>
</soap11:Envelope>
 
//formatted for readability
```

### 基于REST的结构化资源 {#rest-based-struct-resource}

一些MVPD已对以下基于REST的授权协议进行了标准化。 此方法与XACML方法一样具有完整的功能，但提供了“更轻量”的实施。

`// The MRSS is base64 encoded by Adobe Primetime authentication, and passed in that format to the REST-based Authorization endpoint.`

`https://auth.somedomain.net/mediation/1/rest/client/authz?uuID=AC82CE4&mrss=base64encodedstring&IPAddress=123.456.78.901`

<!--
>[!RELATEDINFORMATION]
>* [User Metadata Exchange](/help/authentication/mvpd-user-metadata-exchng.md)
>* [Logout](/help/authentication/usecase-mvpd-logout.md)
>* [Programmer Integration Guide: Identifying Protected Resources](/help/authentication/identify-protected-resources.md)
>* [Programmer Integration Guide: User Metadata Exchange](/help/authentication/user-metadata.md)
-->