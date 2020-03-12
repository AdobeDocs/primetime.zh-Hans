---
description: TVSDK以XML格式向Adobe发送计费指标。
seo-description: TVSDK以XML格式向Adobe发送计费指标。
seo-title: 传输付费指标
title: 传输付费指标
uuid: c925800c-0fb7-4781-94e8-7e7ad94bb965
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 传输付费指标 {#transmit-billing-metrics}

TVSDK以XML格式向Adobe发送计费指标。

<!--<a id="example_13ABDB1CC0B549968A534765378DA3A0"></a>-->

如果使用网络捕获工具监视TVSDK传输到Adobe的统计信息，您应看到如下单元：

```xml
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

布尔属 `drmProtected`性， `adsEnabled`仅在 `midrollEnabled` 为true时才显示。