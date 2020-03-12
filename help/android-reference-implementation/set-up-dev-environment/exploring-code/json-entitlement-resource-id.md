---
seo-title: 授权资源ID的JSON对象
title: 授权资源ID的JSON对象
uuid: f5b659da-1732-404c-bf00-d32a0ae39aa1
description: 当授权资源ID是简单的文本字符串时，以下代码块提供了JSON对象的示例。
seo-description: 当授权资源ID是简单的文本字符串时，以下代码块提供了JSON对象的示例。
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# 授权资源ID的JSON对象 {#json-object-for-entitlement-resource-id}

当授权资源ID是简单的文本字符串时，以下代码块提供了JSON对象的示例。 在这种情况下，资源ID是字符串“resource”。

```
"metadata" : { 
"entitlement" : { 
"id" : "resource" 
} 
}
```

当授权资源ID是HTML编码的mRSS字符串时，以下代码块提供JSON对象的示例。

```
<rss version="2.0" xmlns:media="https://search.yahoo.com/mrss/"> 
<channel> 
<title>REF_ADOBE</title> 
<item> 
<title>Adobe Primetime Reference</title> 
<guid>1234</guid> 
<media:rating scheme="urn:v-chip">TV-PG</media:rating> 
</item> 
</channel> 
</rss>
```

以下mRSS字符串用作资源ID。

```
"metadata" : { 
    "entitlement" : { 
        "id" : "<rss version=&quot;2.0&quot; 
        xmlns:media=&quot; 
        https://search.yahoo.com/mrss/&quot; 
        ><channel><title>REF_ADOBE</title><item> 
        <title>Adobe Primetime Reference</title><guid> 
        1234</guid><media:rating scheme=&quot;urn:v-chip&quot;> 
        TV-PG</media:rating></item></channel></rss>" 
        } 
} 
```
