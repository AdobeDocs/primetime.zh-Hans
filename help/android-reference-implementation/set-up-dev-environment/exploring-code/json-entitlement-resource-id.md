---
title: 授权资源ID的JSON对象
description: 以下代码块提供了权利资源ID为简单文本字符串时的JSON对象示例。
exl-id: 396c43e7-404a-40f5-8113-a720e2c834e7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---

# 授权资源ID的JSON对象 {#json-object-for-entitlement-resource-id}

以下代码块提供了权利资源ID为简单文本字符串时的JSON对象示例。 在这种情况下，资源ID是字符串“resource”。

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
