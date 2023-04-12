---
title: 通过被动身份验证的单点登录
description: 通过被动身份验证的单点登录
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 0%

---


# 通过被动身份验证的单点登录

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。


## 简介

本文档的范围是介绍被动身份验证流程的实施，以及这如何与我们标准的单点登录方法配合使用。

## 用例

Adobe Primetime身份验证允许应用程序/站点之间的单点登录(SSO)。 用户使用其MVPD凭据登录后，Adobe Primetime身份验证会生成一个表示MVPD身份验证会话的安全令牌，并使用设备ID将该令牌绑定到用户的设备。 Adobe Primetime身份验证会将令牌/设备ID存储在服务器或设备上。

只要令牌仍然有效，用户就会直接显示为已通过身份验证。 这样，用户在确保交易安全的同时，可以更少地输入其凭据。



此处详述的业务用例是一个非常具体的要求：每个访问的网站必须至少对用户进行一次身份验证。 这使MVPD能够应用与authN会话关联的业务规则，这些规则可能因网络而异。 它与当前TVE的承诺相冲突，即用户只需登录一次，即可在属于Adobe Primetime身份验证生态系统的所有站点上进行身份验证。



为了维护业务规则并保持良好的用户体验，MVPD不要求用户手动提供凭据信息。 我们可以从之前设置的会话Cookie中受益，并尝试使用被动流进行自动重新身份验证；从用户角度看，他将显示为自动登录。



为了解决这些问题，我们实施了2个不同的功能：每个网络的身份验证和被动身份验证支持。 MVPD将支持SAML被动authN，无论该会话是在哪个网站上创建的，如果IdP上存在authN会话，则MVPD只需在该用户的身份验证上重新验证。



## 每个网络的身份验证

此功能可确保MVPD收到每个访问站点的验证请求一次。 此功能意味着Adobe Primetime身份验证令牌将绑定到请求者ID，因此仅对请求该令牌的网络有效。 因此，用户在网站“A”上进行身份验证后，随后访问网站“B”，将需要进行身份验证。



请注意，由于用户在MVPD IdP上已进行了身份验证，因此不需要用户提供登录信息，而是只需将浏览器从站点“B”重定向到MVPD IdP，然后重定向回来。 如果同一用户返回，则仍会在网站“A”上对其进行身份验证。



以下流程描述了“按网络进行身份验证”的基本功能：





## 被动身份验证

这样做的目的是使重新身份验证过程在后台进行，而无需完全重定向浏览器并显示选取器。 因此，从网站A移动到网站B的用户将自动进行身份验证。



从UX的角度来看，此流与使用常规MVPD执行的流之间没有区别。 用户看到的是，在因访问网站A而输入凭据后，将在网站B上自动进行身份验证。



为了使此流程可行，MVPD将需要支持被动身份验证，以便在MVPD不再具有会话的情况下，隐藏的iframe不会“卡住”在登录页面上。 这是通过标准“isPassive”属性完成的。



下图描述了改进的流程和“后台”被动身份验证：





SAML请求示例以下是被动authN流的SAML请求示例：


```xml
<saml2p:AuthnRequest xmlns:saml2p="urn:oasis:names:tc:SAML:2.0:protocol"
                     AssertionConsumerServiceURL="https://sp.auth.adobe.com/sp/saml/SAMLAssertionConsumer"
                     Destination="https://mvpd_idp_url"
                     ForceAuthn="false"
                     ID="_15056686-399c-4528-b21a-4a9542cfc8ec"
                     IsPassive="true"
                     IssueInstant="2014-11-03T14:18:12.394Z"
                     ProtocolBinding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-POST"
                     Version="2.0"
                     >
    <saml2:Issuer xmlns:saml2="urn:oasis:names:tc:SAML:2.0:assertion">https://saml.sp.auth.adobe.com </saml2:Issuer>
    <saml2p:Extensions>
        <thrpty:RespondTo xmlns:thrpty="urn:oasis:names:tc:SAML:protocol:ext:third-party">https://saml.sp.auth.adobe.com</thrpty:RespondTo>
    </saml2p:Extensions>
    <saml2p:NameIDPolicy AllowCreate="true"
                         Format="urn:oasis:names:tc:SAML:2.0:nameid-format:transient"
                         SPNameQualifier="https://saml.sp.auth.adobe.com"
                         />
</saml2p:AuthnRequest>
```

业务规则MVPD具有特定的SSO范围限制域。 例如，某些MVPD(同一媒体公司的单点登录(SSO)，但不能跨公司)只允许某些域。
某些MVPD可能要求强制使用不同的身份验证规则。 例如，MVPD的身份验证TTL可能因不同网络而异。 此外，MVPD可能会为某些网络启用基于家庭的身份验证，但不能为其他网络启用基于家庭的身份验证（此处强烈显示家长控制用例）。


这些业务要求应当记住，主要用例是，用户在成功使用其MVPD登录后，不应被要求再次登录。

这可以通过使用带有被动authN标记的每个网络的身份验证来实现。



iOS的已知限制 — 由于iOS本地存储的性质，SSO流在iOS上不适用于由不同供应商开发的应用程序。 有关iOS 8及更高版本中单点登录(SSO)的详细信息，请参阅此技术说明。


<!--
>[!RELATEDINFORMATION]
>* Single Sign-On on iOS
>* SSO on iOS when using the Primetime authentication Access Enabler
-->