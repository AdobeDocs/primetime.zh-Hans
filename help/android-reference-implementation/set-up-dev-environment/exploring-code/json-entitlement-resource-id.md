---
title: 授权资源ID的JSON对象
description: 以下代码块提供了授权资源ID为简单文本字符串时的JSON对象示例。
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---

# 授权资源ID的JSON对象 {#json-object-for-entitlement-resource-id}

以下代码块提供了授权资源ID为简单文本字符串时的JSON对象示例。 在本例中，资源ID是字符串“resource”。

```
"metadata" : { 
"entitlement" : { 
"id" : "resource" 
} 
}
```

以下代码块提供了授权资源ID是HTML编码的mRSS字符串时的JSON对象示例。

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
