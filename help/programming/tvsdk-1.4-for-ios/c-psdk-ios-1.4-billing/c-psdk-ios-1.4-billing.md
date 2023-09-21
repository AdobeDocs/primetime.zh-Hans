---
description: 为了适应那些只想按客户所使用内容支付而不是不管实际使用情况都按固定费率支付的客户，Adobe会收集使用情况量度，并使用这些量度来确定向客户收取多少费用。
title: 计费量度
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# 计费量度 {#billing-metrics}

为了适应那些只想按客户所使用内容支付而不是不管实际使用情况都按固定费率支付的客户，Adobe会收集使用情况量度，并使用这些量度来确定向客户收取多少费用。

每次播放器生成流启动事件时，TVSDK就会开始定期向Adobe计费系统发送HTTP消息。 该时段（称为可计费持续时间）对于标准VOD、专业VOD（启用中置广告）和实时内容可能不同。 每种内容类型的默认持续时间为30分钟，但实际值由您的Adobe合同确定。

这些消息包含以下信息：

* 内容类型（实时、线性或VOD）
* 内容URL
* 是否启用广告
* 是否启用中置广告（仅限VOD）
* 流是否受DRM保护
* TVSDK版本和平台

Adobe会预配置此安排，但如果要更改安排，请与您的Adobe启用代表合作。

要监控TVSDK发送到Adobe的统计信息，请从Adobe启用代表处获取URL，然后使用网络捕获工具（例如Charles）查看数据。

## 配置计费量度 {#configure-billing-metrics}

如果您使用默认配置，则无需执行任何其他操作即可启用或配置计费。 如果您从“Adobe启用”代表处获取了不同的配置参数，请在初始化媒体播放器之前使用PTBillingMetricsConfiguration类设置这些参数。

大多数客户应使用默认配置。

>[!IMPORTANT]
>
>您设置的配置将在媒体播放器的生命周期内保持有效。 初始化媒体播放器后，便无法更改配置。

要配置计费指标，请执行以下操作：

1. 输入以下代码示例。

   ```
   PTBillingMetricsConfiguration *billingConfig = [[[PTBillingMetricsConfiguration alloc] init] autorelease]; 
   billingConfig.enabled = YES; 
   billingConfig.stdVODBillableDurationMinutes = 60.0; 
   billingConfig.proVODBillableDurationMinutes = 30.0; 
   billingConfig.liveBillableDurationMinutes = 15.0; 
   
   // metadata is the PTMetadata instance set on PTMediaPlayerItem 
   [metadata setMetadata:billingConfig forKey:PTBillingMetricsConfigurationMetadataKey];
   ```

## 传输计费指标 {#transmit-billing-metrics}

TVSDK以XML格式将计费指标发送给Adobe。

<!--<a id="example_13ABDB1CC0B549968A534765378DA3A0"></a>-->

如果使用网络捕获工具监视TVSDK传输到Adobe的统计信息，您应看到如下单位：

```
<request> 
     <sc_xml_ver>1.0</sc_xml_ver> 
     <reportSuiteID>ptebilling</reportSuiteID> 
     <visitorID>5536C629-5EF7-4F02-8E5D-9FA136CB3CED</visitorID> 
     <pageName>com.adobe.primetime.psdksample</pageName> 
     <timestamp>2016-11-22T18:06:30+0000</timestamp> 
     <userAgent>Mozilla/5.0 (iPad; CPU OS 9_1 like Mac OS X) AppleWebKit/601.1.46 (KHTML, like Gecko) Mobile/13B143</userAgent> 
     <contextData> 
         <billingMetrics> 
                 <contentDuration>1799111</contentDuration> 
                 <contentURL>https%3A%2F%2Fdevimages.apple.com.edgekey.net%2Fstreaming%2Fexamples%2Fbipbop_16x9%2Fbipbop_16x9_variant.m3u8</contentURL> 
                 <contentType>vod</contentType> 
                 <midrollEnabled>true</midrollEnabled> 
                 <tvsdkVersion>1.0.211</tvsdkVersion> 
                 <platform>Mozilla/5.0 (iPad; CPU OS 9_1 like Mac OS X) AppleWebKit/601.1.46 (KHTML, like Gecko) Mobile/13B143</platform> 
                 <publisherID>com.adobe.primetime.psdksample</publisherID> 
                 <adsEnabled>true</adsEnabled> 
                 <type>start</type> 
         </billingMetrics> 
     </contextData> 
</request>
```

布尔值属性 `drmProtected`， `adsEnabled`、和 `midrollEnabled` 仅当它们为true时才显示。
