---
title: 授权资源ID的JSON对象
description: 当授权资源ID是简单文本字符串时，以下代码块提供了JSON对象的示例。
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 0%

---


# 授权资源ID {#json-object-for-entitlement-resource-id}的JSON对象

当授权资源ID是简单文本字符串时，以下代码块提供了JSON对象的示例。 在这种情况下，资源ID是字符串&quot;resource&quot;。

```
"metadata" : { 
"entitlement" : { 
"id" : "resource" 
} 
}
```

当授权资源ID是HTML编码的mRSS字符串时，以下代码块提供了JSON对象的示例。

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
