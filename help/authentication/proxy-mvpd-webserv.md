---
title: 代理MVPD Web服务
description: 代理MVPD Web服务
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 0%

---


# 代理MVPD Web服务 {#proxy-mvpd-wbservice}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## 概述 {#overview-proxy-mvpd-webserv}

“代理MVPD”是指MVPD，除了管理与Adobe Primetime身份验证的集成外，还代表一组关联的“代理MVPD”来管理授权流程。 此安排对程序员是透明的。

为了实施ProxyMVPD功能，Adobe Primetime身份验证提供RESTful Web服务，ProxyMVPD可通过这些服务提交和检索ProxiedMVPD的列表。 此公共API使用的协议为REST HTTP，其假设如下：

* 代理MVPD使用HTTPGET方法检索当前集成的MVPD的列表。
* 代理MVPD使用HTTPPOST方法来更新支持的MVPD的列表。

## 代理MVPD服务 {#proxy-mvpd-services}

* [检索代理的MVPD](#retriev-proxied-mvpds)
* [提交代理的MVPD](#submit-proxied-mvpds)

### 检索代理的MVPD {#retriev-proxied-mvpds}

检索由apikey参数标识的ProxyMVPD的代理MVPD的当前列表。

| 端点 | 调用者 | 请求标头 | HTTP方法 | HTTP响应 |
|---|---|---|---|---|
| &lt;fqdn>/control/v1/proxiedMvpds | ProxyMVPD | apikey（必填） | GET | <ul><li> 200（确定） — 请求已成功处理，且响应包含XML格式的ProxiedMVPD列表</li><li>401（未授权） — 对提供的凭据要求用户身份验证或未授予授权。  指示以下任一情况：<ul><li>请求标头中不存在Apikey令牌</li><li>请求源自允许列表中不存在的IP地址</li><li>令牌无效</li></ul></li><li>403（禁止） — 指示所提供参数不支持该操作，或者代理MVPD未设置为代理或缺少代理</li><li>405（不允许使用方法） — 使用HTTP方法而不是GET或POST。 通常不支持HTTP方法，或者此特定端点不支持HTTP方法。</li><li>500（内部服务器错误） — 在请求过程中在服务器端引发错误。</li></ul> |

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
| &lt;fqdn>/control/v1/proxiedMvpds | ProxyMVPD | apikey（必需）proxied-mvpds（必需） | POST | <ul><li>201（已创建） — 已成功处理推送</li><li>400（请求错误） — 服务器不知道如何处理请求：<ul><li>传入XML不符合此规范中发布的架构</li><li>代理的mvpd没有唯一ID</li><li>400响应代码的推送请求者ID不存在其他Servlet容器原因</li></ul><li>401（未授权） — 该apikey无效或呼叫者IP不在允许列表上</li><li>403（禁止） — 指示所提供参数不支持该操作，或者代理MVPD未设置为代理或缺少代理</li><li>405（不允许使用方法） — 使用HTTP方法而不是GET或POST。 通常不支持HTTP方法，或者此特定端点不支持HTTP方法。</li><li>500（内部服务器错误） — 在请求过程中在服务器端引发错误。</li></ul> |

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


### 发帖频度 {#posting-frequency}

Adobe Primetime身份验证建议ProxyMVPD仅在与上一个推送发生更改时，才应推送其代理MVPD列表。

### 删除代理的MVPD {#delete-proxied-freqency}

如果ProxyMVPD推送XML记录，且该XML记录的ProxiedMVPD为空，则该空清单将像任何清单一样存储在我们的系统中，从而有效地删除前一个清单。



## XSD格式 {#xsd-format}

Adobe已定义了以下可接受的格式，用于将代理MVPD从/检索到我们的公共Web服务：

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

**有关元素的说明：**

* `id` （必需） — 代理的MVPD ID必须是与MVPD名称相关的字符串，并使用以下任意字符（因为出于跟踪目的，程序员会看到该字符）：
   * 任何字母数字字符、下划线(&quot;_&quot;)和连字符(&quot;-&quot;)。
   * idID必须符合以下正则表达式：
      `(a-zA-Z0-9((-)|_)*)`

      因此，它必须至少有一个字符，以字母开头，并以任何字母、数字、短划线或下划线继续。

* `iframeSize` （可选） — iFrameSize元素是可选的，并且定义如果MVPD身份验证页面应位于iFrame中，则iFrame的大小。 否则，如果iframeSize元素不存在，则会在整个浏览器重定向页面中进行身份验证。
* `requestorIds` （可选） — 请求者IDS值将由Adobe提供。 要求将代理的MVPD与至少一个请求者ID相集成。 如果代理的MVPD元素上不存在“requestorIds”标记，则代理的MVPD将与集成在代理MVPD下的所有可用请求者集成。
* `ProviderID` （可选） — 当id元素上存在ProviderID属性时，ProviderID的值将在SAML身份验证请求中作为代理MVPD/SubMVPD ID（而不是id值）发送给代理MVPD。 在这种情况下，ID的值将仅用于“程序员”页面上显示的MVPD选取器中，并在内部通过Adobe Primetime身份验证来使用。 ProviderID属性的长度必须介于1到128个字符之间。

## 安全性 {#security}

请求被视为有效，必须遵守以下规则：

* 请求标头必须包含安全apikey参数。 （这是一个将唯一标识代理MVPD调用的应用程序密钥。）
* 请求必须来自允许的特定IP地址。
* 必须通过SSL协议发送请求。

Adobe将提供令牌的（静态）值。 此值用于身份验证和授权过程。  请求标头中存在且上面未列出的任何参数都将被忽略。

Curl示例：

`curl -X GET -H "apikey: ???provided-by-adobe???" "https://mgmt-prequal.auth-staging.adobe.com/control/v1/proxiedMvpds"`

## Adobe Primetime身份验证环境的代理MVPD Web服务端点 {#proxy-mvpd-wevserv-endpoints}

* **生产URL:** https://mgmt.auth.adobe.com/control/v1/proxiedMvpds
* **暂存URL:** https://mgmt.auth-staging.adobe.com/control/v1/proxiedMvpds
* **预准生产URL:** https://mgmt-prequal.auth.adobe.com/control/v1/proxiedMvpds
* **暂存前URL:** https://mgmt-prequal.auth-staging.adobe.com/control/v1/proxiedMvpds

<!--
>[!RELATEDINFORMATION]
>* [Proxy MVPD SAML integration](/help/authentication/proxy-mvpd-saml-int.md)
>* [User metadata exchange](/help/authentication/mvpd-user-metadata-exchng.md)
>* [Technical paper](/help/authentication/technical-paper.md)
>* [Adobe Primetime Authentication glossary](/help/authentication/glossary.md)
-->
