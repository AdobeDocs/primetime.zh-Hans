---
description: 浏览器TVSDK以XML格式向Adobe发送计费量度。
title: 传输付费量度
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '61'
ht-degree: 0%

---


# 传输计费量度{#transmit-billing-metrics}

浏览器TVSDK以XML格式向Adobe发送计费量度。

<!--<a id="example_13ABDB1CC0B549968A534765378DA3A0"></a>-->

如果使用网络捕获工具来监视浏览器TVSDK传输到Adobe的统计信息，您应看到以下单位：

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

布尔属性`drmProtected`、`adsEnabled`和`midrollEnabled`仅在为true时才显示。