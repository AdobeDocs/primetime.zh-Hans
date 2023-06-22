---
description: TVSDK以XML格式将计费指标发送到Adobe。
title: 传输计费指标
exl-id: 55009ce6-a814-4a20-bfa5-e8cf2d7ba923
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '58'
ht-degree: 0%

---

# 传输计费指标 {#transmit-billing-metrics}

TVSDK以XML格式将计费指标发送到Adobe。

<!--<a id="example_13ABDB1CC0B549968A534765378DA3A0"></a>-->

如果使用网络捕获工具监视TVSDK传输到Adobe的统计信息，您应看到如下单位：

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

布尔属性 `drmProtected`， `adsEnabled`、和 `midrollEnabled` 仅在为真时显示。
