---
title: MVPD用户元数据交换
description: MVPD用户元数据交换
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 0%

---


# MVPD用户元数据交换

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## 简介 {#intro-user-metadata-exchange}

MVPD会维护与其客户有关的特定于用户的元数据，在某些情况下，这些元数据会与程序员共享。 Adobe Primetime身份验证的目的是为此“用户元数据”的交换代理，但不是强制执行任何类型的交换规则。 交换规则是让MVPD与其程序员合作伙伴一起制定的。

当前可用于交换的用户元数据类型包括：

* 邮政编码
* 最高评级（VChip或MPAA）
* 用户ID
* 家庭ID
* 渠道ID

使用此功能，MVPD和程序员可以实施特殊用例，如家长控制。 例如，MVPD可以将家长评级数据传递给程序员，程序员随后使用该数据过滤用户可用的查看选项。

用户元数据关键点：

* MVPD在验证和授权流程期间将用户元数据传递到程序员的应用程序
* Adobe Primetime身份验证会将元数据值保存在AuthN和AuthZ令牌中
* Adobe Primetime身份验证可以标准化MVPD的值，这些值以不同格式提供用户元数据
* 某些参数可以使用程序员的密钥加密
* 特定值由Adobe通过配置更改提供

>[!NOTE]
>
>用户元数据是以前在Adobe Primetime身份验证中提供的静态元数据（身份验证令牌TTL、授权令牌TTL和设备ID）的扩展。

## 示例 {#example-mvpd-user-metadata-exch}

### 家长控制 {#example-parental-control}

此示例显示了以下内容的更改：

* [MVPD元数据交换程序员](#progr-mvpd-metadata-exch)

* [MVPD到程序员元数据交换流](#mvpd-progr-exchange-flow)

### MVPD元数据交换程序员 {#progr-mvpd-metadata-exch}

目前，程序员API、Adobe Primetime身份验证和MVPD授权程序均仅支持通道级别的授权。 在程序员的getAuthorization()API调用中，该渠道被指定为纯文本字符串。 此字符串会一直传播到MVPD的授权后端：

从程序员的应用程序或网站中，用户选择支持XACML的MVPD（在本例中为“TNT”）。 有关XACML的信息，请参阅 [扩展访问控制标记语言](https://en.wikipedia.org/wiki/XACML){target=_blank}.
程序员应用程序会形成一个AuthZ请求，其中包含该资源及其元数据。  此示例包括渠道元素的媒体属性中的美国电影协会(MPAA)评级为“pg”：

```XML
var resource = '<rss version="2.0" xmlns:media="http://video.search.yahoo.com/mrss/">
                    <channel> 
                        <title>TNT</title> 
                        <media:rating scheme="urn:mpaa">pg</media:rating>
                    </channel>
                </rss>';
getAuthorization(resource);
```

Adobe Primetime身份验证实际上支持更精细的授权（在MVPD和程序员都支持的情况下，可精确到资产级别）。 资源及其元数据是不透明的，不可Adobe;其目的是建立一种标准格式，用于以标准化方式指定资源ID和元数据，以将资源ID发送到不同的MVPD。

>[!NOTE]
>
>如果用户选择仅支持渠道的MVPD，则Adobe Primetime身份验证仅提取渠道标题（上例中为“TNT”），并仅将标题传递给MVPD。

### MVPD到程序员元数据交换流 {#mvpd-progr-exchange-flow}

Adobe Primetime身份验证做出以下假设：

* MVPD将作为SAML响应的一部分发送最大评级
* 此信息将作为身份验证令牌的一部分保存
* 由Adobe Primetime身份验证提供的API使程序员能够检索此信息
* 程序员在其网站或应用程序上实施此功能（例如，隐藏超出用户最高评分的视频）

```XML
<saml:Assertion ID="pfxec5f92e0-8589-3fc3-c708-f4fb8e2fad59"
                 IssueInstant="2010-07-20T10:05:41Z" Version="2.0"
                 xmlns:xs="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <saml:AttributeStatement>
        <saml:Attribute
                Name="MaxTVRating"
                NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
            <saml:AttributeValue xsi:type="xs:string">tv-ma</saml:AttributeValue>
        </saml:Attribute>
        <saml:Attribute
                Name="MaxMovieRating"
                NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
            <saml:AttributeValue xsi:type="xs:string">nc-17</saml:AttributeValue>
        </saml:Attribute>
    </saml:AttributeStatement>
</saml:Assertion>
```

### 注释 {#notes-mvpd-progr-metadata-exch-flow}

**资源标准化和验证。** 资源ID可以作为纯字符串或MRSS字符串进行传递。 程序员可以决定使用纯字符串格式或MRSS，但需要先与MVPD达成协议，以便MVPD知道如何处理该资源。

**资源ID和元数据规范。** Adobe Primetime身份验证将RSS标准与Media RSS扩展结合使用来指定资源及其元数据。 与Media RSS扩展一起，Adobe Primetime身份验证支持多种元数据，例如家长控制(通过 `<media:rating>`)或地理位置(`<media:location>`)。

Adobe Primetime身份验证还可支持从旧版渠道字符串到需要RSS的MVPD的相应RSS资源的透明转换。 另一方面，对于仅通道MVPD，Adobe Primetime身份验证支持从RSS+MRSS转换为纯通道标题。

**Adobe Primetime身份验证可确保与现有集成完全向后兼容。** 也就是说，对于使用渠道级别身份验证的程序员，在将渠道ID发送到了解该格式的MVPD之前，Adobe Primetime身份验证会注意以必要的格式打包渠道ID。 反过来也适用：如果程序员以新格式指定其所有资源，则Adobe Primetime身份验证会将新格式转换为简单的渠道字符串（如果针对仅执行渠道级别授权的MVPD进行授权）。

## 用户元数据用例 {#user-metadata-use-cases}

随着越来越多的MVPD进行法律安排并添加功能，用例会不断变化和扩展。 以下是可用于哪些用户元数据的示例。

* [MVPD用户ID](#mvpd-user-id)
* [家庭ID](#household-user-id)
* [邮政编码](#zip-code)
* [最大评分（家长控制）](#max-rating-parental-control)
* [渠道阵容](#channel-line-up)

### MVPD用户ID {#mvpd-user-id}

* 由MVPD提供
* 不是用户的实际登录信息，因为该信息由MVPD进行哈希处理
* 可用于指示特定用户遇到或遇到的问题
* 加密
* MVPD支持：所有MVPD

### 家庭用户ID {#household-user-id}

* 允许获取良好的量度信息
* 加密
* MVPD支持：一些MVPD

### 邮政编码 {#zip-code}

* 用户的账单邮政编码
* 主要用于执行体育赛事冻结期规则
* 可以随AuthZ响应一起提供，以便进行快速更新
* MVPD支持：一些MVPD

### 最大评分（家长控制） {#max-rating-parental-control}

* 初始验证N，加上验证Z刷新
* 从UI中筛选内容
* 美国电影协会或VChip评级
* MVPD支持：一些MVPD

### 渠道阵容 {#channel-line-up}

* MVPD可以提供用户有权查看的渠道列表
* 允许快速进行UI绘画
* OLCA规范允许在AuthN响应中将此作为AttributeStatement
* 支持MVPD:一些MVPD

<!--
>[!RELATEDINFORMATION]
>
>* [Proxy MVPD Web Service](/help/authentication/proxy-mvpd-webserv.md)
>* [Content Metadata Exhange](/help/authentication/mvpd-content-metadata-exchange.md)
>* [OLCA AuthN / AuthZ Specification](https://www.cablelabs.com/specifications/CL-SP-AUTH1.0-I04-120621.pdf){target=_blank}
>* [User Metadata (Programmer Integration Guide)](/help/authentication/user-metadata-feature.md)
-->
