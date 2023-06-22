---
title: 代理MVPD Web服务
description: 代理MVPD Web服务
exl-id: f75cbc4d-4132-4ce8-a81c-1561a69d1d3a
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 0%

---

# 代理MVPD Web服务 {#proxy-mvpd-wbservice}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权的使用。

## 概述 {#overview-proxy-mvpd-webserv}

“代理MVPD”是一个MVPD，它除了管理自身与Adobe Primetime身份验证的集成之外，还代表一组关联的“代理MVPD”管理授权过程。 这种安排对程序员是透明的。

为实施ProxyMVPD功能，Adobe Primetime身份验证提供RESTful Web服务，ProxyMVPDs可以使用该服务提交和检索ProxiedMVPDs列表。 用于此公共API的协议是REST HTTP，带有以下假设：

* 代理MVPD使用HTTPGET方法检索当前集成MVPD的列表。
* 代理MVPD使用HTTPPOST方法更新支持的MVPD列表。

## 代理MVPD服务 {#proxy-mvpd-services}

* [检索代理的MVPD](#retriev-proxied-mvpds)
* [提交代理的MVPD](#submit-proxied-mvpds)

### 检索代理的MVPD {#retriev-proxied-mvpds}

检索由apikey参数标识的ProxyMVPD的当前代理MVPD列表。

| 端点 | 调用者 | 请求标头 | HTTP方法 | HTTP响应 |
|---|---|---|---|---|
| &lt;fqdn>/control/v1/proxiedMvpds | ProxyMVPD | apikey（必需） | GET | <ul><li> 200 （确定） — 已成功处理请求，响应包含XML格式的ProxiedMVPD列表</li><li>401（未授权） — 需要用户身份验证或提供的凭据未获得授权。  指示以下任一项：<ul><li>请求标头中不存在apikey令牌</li><li>请求源自允许列表中不存在的IP地址</li><li>令牌无效</li></ul></li><li>403 （禁止） — 指示提供的参数不支持该操作，或者代理MVPD未设置为代理或丢失</li><li>405（不允许使用该方法） — 使用的HTTP方法不是GET或POST。 HTTP方法通常不受支持，或者此特定端点不支持。</li><li>500（内部服务器错误） — 在请求过程中，在服务器端引发了一个错误。</li></ul> |

Curl示例：

`curl -X GET -H "apikey: ???provided-by-adobe???" "https://mgmt-prequal.auth-staging.adobe.com/control/v1/proxiedMvpds"`


XML响应示例：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<proxiedMvpds>
    <proxiedMvpd>
        <id>oneMvpdId</id>
        <displayName>MVPD Name</displayName>
        <logoURL></logoURL>
    </proxiedMvpd>
    <proxiedMvpd>
        <id ProviderID="ProviderID_Value_Sent_On_IdPEntry">mvpdPickerId</id>
        <displayName>MVPD Name Two</displayName>
        <logoURL></logoURL>
        <requestorIds>
            <requestorId>TheRequestorId_IntegratedWith</requestorId>
        </requestorIds>
    </proxiedMvpd>
    <proxiedMvpd>
        <id>anotherMvpdId</id>
        <displayName>Another MVPD</displayName>
        <logoURL></logoURL>
        <iframeSize>
            <iframeHeight>400</iframeHeight>
            <iframeWidth>340</iframeWidth>
        </iframeSize>
        <requestorIds>
            <requestorId>FirstIntegratedRequestorId</requestorId>
            <requestorId>SecondIntegratedRequestorId</requestorId>
        </requestorIds>
    </proxiedMvpd>
</proxiedMvpds>
```

### 提交代理的MVPD {#submit-proxied-mvpds}

推送与由apikey参数标识的代理MVPD集成的MVPD数组。

| 端点 | 调用者 | 请求标头 | HTTP方法 | HTTP响应 |
|:------------------------------:|:---------:|:--------------------------------------------:|:-----------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| &lt;fqdn>/control/v1/proxiedMvpds | ProxyMVPD | apikey（必需）proxied-mvpds（必需） | POST | <ul><li>201（已创建） — 已成功处理推送</li><li>400（错误请求） — 服务器不知道如何处理该请求：<ul><li>传入的XML不符合此规范中发布的架构</li><li>代理的mvpds没有唯一id</li><li>推送的requestorId不存在400响应代码的其他Servlet容器原因</li></ul><li>401 （未授权） - apikey无效或调用方IP不在允许列表上</li><li>403 （禁止） — 指示提供的参数不支持该操作，或者代理MVPD未设置为代理或丢失</li><li>405（不允许使用该方法） — 使用的HTTP方法不是GET或POST。 HTTP方法通常不受支持，或者此特定端点不支持。</li><li>500（内部服务器错误） — 在请求过程中，在服务器端引发了一个错误。</li></ul> |

Curl示例：

`curl -X POST -H "apikey: <API_KEY>" "https://mgmt-prequal.auth.adobe.com/control/v1/proxiedMvpds" -d "proxied-mvpds=%3CproxiedMvpds%3E%3CproxiedMvpd%3E%3CdisplayName%3EFirst%20MVPD%20Name%3C%2FdisplayName%3E%3Cid%3EfirstMVPDId%3C%2Fid%3E%3ClogoURL%3E%3C%2FlogoURL%3E%3C%2FproxiedMvpd%3E%3CproxiedMvpd%3E%3Cid%20ProviderID%3D%22ProviderID_Value_Sent_On_IdPEntry%22%3EmvpdPickerId%3C%2Fid%3E%3CdisplayName%3EMVPD%20Name%20Two%3C%2FdisplayName%3E%3ClogoURL%3E%3C%2FlogoURL%3E%3CrequestorIds%3E%3CrequestorId%3ETHE_REQUESTOR_ID%3C%2FrequestorId%3E%3C%2FrequestorIds%3E%3C%2FproxiedMvpd%3E%3C%2FproxiedMvpds%3E"`



XML示例：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<proxiedMvpds>
    <proxiedMvpd>
        <id>oneMvpdId</id>
        <displayName>MVPD Name</displayName>
        <logoURL></logoURL>
    </proxiedMvpd>
    <proxiedMvpd>
        <id ProviderID="ProviderID_Value_Sent_On_IdPEntry">mvpdPickerId</id>
        <displayName>MVPD Name Two</displayName>
        <logoURL></logoURL>
        <requestorIds>
            <requestorId>TheRequestorId_IntegratedWith</requestorId>
        </requestorIds>
    </proxiedMvpd>
    <proxiedMvpd>
        <id>anotherMvpdId</id>
        <displayName>Another MVPD</displayName>
        <logoURL></logoURL>
        <iframeSize>
            <iframeHeight>400</iframeHeight>
            <iframeWidth>340</iframeWidth>
        </iframeSize>
        <requestorIds>
            <requestorId>FirstIntegratedRequestorId</requestorId>
            <requestorId>SecondIntegratedRequestorId</requestorId>
        </requestorIds>
    </proxiedMvpd>
</proxiedMvpds>
```


### 过帐频率 {#posting-frequency}

Adobe Primetime身份验证建议ProxyMVPDs仅在上一次推送发生更改时推送其ProxiedMVPD列表。

### 删除代理的MVPD {#delete-proxied-freqency}

如果ProxyMVPD推送具有空ProxiedMVPDs列表的XML记录，则该空列表将像任何列表一样存储在我们的系统中，从而有效地删除上一个列表。



## XSD格式 {#xsd-format}

Adobe定义了以下可接受的格式，用于向我们的公共Web服务发布/检索代理的MVPD：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"
           xmlns:pxm="http://tve.adobe.com/data/proxiedmvpd"
           targetNamespace="http://tve.adobe.com/data/proxiedmvpd"
           elementFormDefault="qualified"
           version="1.0">
    <xs:complexType name="iframeSize">
        <xs:all>
            <xs:element name="iframeHeight" type="xs:int" minOccurs="1" maxOccurs="1" nillable="false"/>
            <xs:element name="iframeWidth" type="xs:int" minOccurs="1" maxOccurs="1" nillable="false"/>
        </xs:all>
    </xs:complexType>
    <xs:complexType name="requestorIds">
        <xs:annotation>
            <xs:documentation>List of requestors/programmers integrated with the proxied MVPD</xs:documentation>
        </xs:annotation>
        <xs:sequence>
            <xs:element name="requestorId" type="xs:string" minOccurs="1" maxOccurs="unbounded" nillable="false">
                <xs:annotation>
                    <xs:documentation>The requestor/programmer identifier recognized by Adobe</xs:documentation>
                </xs:annotation>
            </xs:element>
        </xs:sequence>
    </xs:complexType>
    <xs:complexType name="proxiedMvpd">
        <xs:all>
            <xs:element name="id" minOccurs="1" maxOccurs="1" nillable="false">
                <xs:annotation>
                    <xs:documentation>The id must conform to the regular expression: ([a-zA-Z0-9]+((\-)|[_])*)</xs:documentation>
                </xs:annotation>
                <xs:complexType>
                    <xs:simpleContent>
                        <xs:extension base="xs:string">
                            <xs:attribute name="ProviderID">
                                <xs:simpleType>
                                    <xs:restriction base="xs:string">
                                        <xs:minLength value="1"/>
                                        <xs:maxLength value="128"/>
                                    </xs:restriction>
                                </xs:simpleType>
                            </xs:attribute>
                        </xs:extension>
                    </xs:simpleContent>
                </xs:complexType>
            </xs:element>
            <xs:element name="displayName" type="xs:string" minOccurs="1" maxOccurs="1" nillable="false"/>
            <xs:element name="logoURL" type="xs:anyURI" minOccurs="1" maxOccurs="1" nillable="false"/>
            <xs:element name="iframeSize" type="pxm:iframeSize" minOccurs="0" maxOccurs="1"/>
            <xs:element name="requestorIds" type="pxm:requestorIds" minOccurs="0" maxOccurs="1"/>
        </xs:all>
    </xs:complexType>
    <xs:element name="proxiedMvpds">
        <xs:annotation>
            <xs:documentation>List of Proxied MVPD</xs:documentation>
        </xs:annotation>
        <xs:complexType>
            <xs:sequence>
                <xs:element name="proxiedMvpd" type="pxm:proxiedMvpd" minOccurs="0" maxOccurs="unbounded"/>
            </xs:sequence>
        </xs:complexType>
    </xs:element>
</xs:schema>
```

**关于要素的附注：**

* `id` （必需） — 代理的MVPD ID必须是与MVPD名称相关的字符串，且使用以下任意字符（因为出于跟踪目的，它将向程序员公开）：
   * 任何字母数字字符、下划线(“_”)和连字符(“ — ”)。
   * idID必须符合以下正则表达式：
      `(a-zA-Z0-9((-)|_)*)`

      因此，它必须至少有一个字符，以字母开头，然后以任意字母、数字、破折号或下划线继续。

* `iframeSize` （可选） — iframeSize元素是可选的，如果应该将MVPD身份验证页面放在iFrame中，它会定义iFrame的大小。 否则，如果iframeSize元素不存在，则会在完整的浏览器重定向页面中进行身份验证。
* `requestorIds` （可选） — requestorIds值将由Adobe提供。 要求代理的MVPD应至少与一个requestorId集成。 如果代理的MVPD元素上不存在“requestorIds”标记，则该代理的MVPD将与在代理MVPD下集成的所有可用请求者集成。
* `ProviderID` （可选） — 当ID元素上存在ProviderID属性时，ProviderID的值将在SAML身份验证请求中作为代理的MVPD/SubMVPD ID发送到代理MVPD（而不是ID值）。 在这种情况下，id的值将仅在“程序员”页面上展示的MVPD选取器中使用，并在内部由Adobe Primetime身份验证使用。 ProviderID属性的长度必须介于1到128个字符之间。

## 安全性 {#security}

请求必须遵循以下规则才能被视为有效：

* 请求标头必须包含安全apikey参数。 （这是一个应用程序密钥，它将唯一标识代理MVPD的调用。）
* 请求必须来自允许的特定IP地址。
* 必须通过SSL协议发送请求。

Adobe将提供令牌的（静态）值。 此值用于身份验证和授权过程。  请求标头中存在但上面未列出的任何参数都将被忽略。

Curl示例：

`curl -X GET -H "apikey: ???provided-by-adobe???" "https://mgmt-prequal.auth-staging.adobe.com/control/v1/proxiedMvpds"`

## Adobe Primetime身份验证环境的代理MVPD Web服务端点 {#proxy-mvpd-wevserv-endpoints}

* **生产URL：** https://mgmt.auth.adobe.com/control/v1/proxiedMvpds
* **暂存URL：** https://mgmt.auth-staging.adobe.com/control/v1/proxiedMvpds
* **预生产URL：** https://mgmt-prequal.auth.adobe.com/control/v1/proxiedMvpds
* **预测试URL：** https://mgmt-prequal.auth-staging.adobe.com/control/v1/proxiedMvpds

<!--
>[!RELATEDINFORMATION]
>* [Proxy MVPD SAML integration](/help/authentication/proxy-mvpd-saml-int.md)
>* [User metadata exchange](/help/authentication/mvpd-user-metadata-exchng.md)
>* [Technical paper](/help/authentication/technical-paper.md)
>* [Adobe Primetime Authentication glossary](/help/authentication/glossary.md)
-->
