---
description: 浏览器TVSDK以XML格式向Adobe发送计费指标。
seo-description: 浏览器TVSDK以XML格式向Adobe发送计费指标。
seo-title: 传输付费指标
title: 传输付费指标
uuid: ed2638d2-7894-4840-b31a-51e48e0a3f49
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---


# 传输计费指标{#transmit-billing-metrics}

浏览器TVSDK以XML格式向Adobe发送计费指标。

<!--<a id="example_13ABDB1CC0B549968A534765378DA3A0"></a>-->

如果您使用网络捕获工具监视浏览器TVSDK传输到Adobe的统计信息，您应看到以下单位：

```
<?xml version="1.0" encoding="UTF-8"?>
<request>
    <sc_xml_ver>1.0</sc_xml_ver>
    <reportSuiteID>primesample2</reportSuiteID>
    <visitorID>947310128cb56f41</visitorID>
    <pageURL>https://. . ..m3u8</pageURL>
    <timestamp>2016-4-7T10:1:4</timestamp>
    <contextData>
        <billingMetrics>
            <publisherID>com.adobe.primetime.reference.PrimetimeReference</publisherID>
            <contentType>vod</contentType>
            <adsEnabled>true</adsEnabled>
            <midrollEnabled>true</midrollEnabled>
            <platform>Mac OSX 10.11.5</platform>
            <tvsdkVersion>2,4,0,1559</tvsdkVersion>
            <contentURL>https://. . ..m3u8</contentURL>
        </billingMetrics>
    </contextData>
</request>
```

布尔属性`drmProtected`、`adsEnabled`和`midrollEnabled`仅在它们为true时才显示。