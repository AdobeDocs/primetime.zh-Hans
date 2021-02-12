---
title: 清单重写和广告获取规则
description: '清单重写和广告获取规则 '
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# 清单重写和广告读取规则{#manifest-rewriting}

PrimetimeAd Insertion能够使用简单的搜索／替换规则重写片段和获取资产。  这可用于将https向下转换为http请求，通过删除TLS握手来提高性能。  这还可用于从同一CDN投放广告资源和cdn资源。

规则定义为常规表达式搜索／替换，可用于在发送前以及插入清单后转换URL。

此示例规则将下载将所有广告请求从https转换为http到domain.com。

```
find: "https://domain.com/(.*)"
replace: "http://domain.com/$1"
```

以下规则将使用内容CDN投放位于Adobe广告存储CDN上的广告。

```
find: "https?://primetime-a.akamaihd.net/(.*)"
replace: "http://mycdn.com/ad-mapping-pathname/$1"
```

可以通过修改BootstrapAPI中的`ptprotoswitch`参数来命名和启用／禁用规则，该参数是要执行的以逗号分隔的规则列表。  例如，可以通过设置`ptprotoswitch=adfetch_rule1,adfetch_rule2`同时执行以下两个规则：

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

请与技术支持联系，为您的帐户创建／启用这些规则。