---
title: 清单重写和广告提取规则
description: 清单重写和广告提取规则
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---

# 清单重写和广告提取规则 {#manifest-rewriting}

PrimetimeAd Insertion能够使用简单的搜索/替换规则重写片段并获取资源。  这可用于将https向下转换为http请求，这将通过删除TLS握手来提高性能。  这还可用于从同一CDN交付广告资产和CDN资产。

规则被定义为正则表达式搜索/替换，可用于在发送url之前以及插入到清单中之后转换url。

此示例规则会将所有广告请求从https向下转换为domain.com http。

```
find: "https://domain.com/(.*)"
replace: "http://domain.com/$1"
```

以下规则将使用内容CDN来投放位于Adobe的广告存储CDN上的广告。

```
find: "https?://primetime-a.akamaihd.net/(.*)"
replace: "http://mycdn.com/ad-mapping-pathname/$1"
```

可以通过修改规则来命名和启用/禁用规则 `ptprotoswitch` BootstrapAPI中的参数，以逗号分隔要执行的规则列表。  例如，这两个规则都可以通过设置来执行 `ptprotoswitch=adfetch_rule1,adfetch_rule2`：

```
<ruleSet>
    <rule name="rule1">
        <find><![CDATA[...]]></find>
        <replace><![CDATA[...]]></replace>
    </rule>
    <rule name="rule2">
        <find><![CDATA[...]]></find>
        <replace><![CDATA[...]]></replace>
    </rule>
</ruleSet>
```

请与技术支持联系，为您的帐户创建/启用这些规则。
