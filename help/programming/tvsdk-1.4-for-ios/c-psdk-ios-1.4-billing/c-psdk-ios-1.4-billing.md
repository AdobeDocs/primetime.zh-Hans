---
description: 为了照顾那些只想为所用内容而非固定费用付费（无论实际用途如何）的客户，Adobe会收集使用量度并使用这些量度来确定向客户收取多少费用。
title: 账单量度
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---


# 帐单量度{#billing-metrics}

为了照顾那些只想为所用内容而非固定费用付费（无论实际用途如何）的客户，Adobe会收集使用量度并使用这些量度来确定向客户收取多少费用。

每次播放器生成流开始事件时，TVSDK开始会定期向Adobe的计费系统发送HTTP消息。 对于标准VOD、专业VOD（启用中间广告）和实时内容，期间（称为可计费持续时间）可以不同。 每种内容类型的默认持续时间为30分钟，但您与Adobe的合同将决定实际值。

这些消息包含以下信息：

* 内容类型（实时、线性或VOD）
* 内容URL
* 是否启用广告
* 是否启用中间广告（仅VOD）
* 流是否受DRM保护
* TVSDK版本和平台

Adobe预配置此安排，但如果要更改此安排，请与Adobe支持代表合作。

要监视TVSDK发送给Adobe的统计信息，请从您的Adobe支持代表处获取URL，并使用网络捕获工具（例如，Charles）查看数据。

## 配置帐单量度{#configure-billing-metrics}

如果您使用默认配置，则无需执行任何其他操作即可启用或配置计费。 如果您从Adobe启用代表获得了不同的配置参数，请在初始化媒体播放器之前使用PTBillingMetricsConfiguration类设置这些参数。

大多数客户应使用默认配置。

>[!IMPORTANT]
>
>您设置的配置在媒体播放器的生命周期内保持有效。 初始化媒体播放器后，便无法更改配置。

要配置开单量度：

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

## 传输计费量度{#transmit-billing-metrics}

TVSDK以XML格式向Adobe发送计费量度。

<!--<a id="example_13ABDB1CC0B549968A534765378DA3A0"></a>-->

如果使用网络捕获工具监视TVSDK传输到Adobe的统计信息，您应看到以下单位：

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

布尔属性`drmProtected`、`adsEnabled`和`midrollEnabled`仅在为true时才显示。