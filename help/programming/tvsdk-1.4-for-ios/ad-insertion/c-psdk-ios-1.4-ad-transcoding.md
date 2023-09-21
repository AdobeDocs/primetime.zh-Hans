---
description: 某些第三方广告（或创意）无法拼合到HTTP实时流(HLS)内容流中，因为其视频格式与HLS不兼容。 Primetime广告插入和TVSDK可以选择尝试将不兼容的广告重新打包到兼容的M3U8视频中。
title: 使用AdobeCreative Repackaging Service重新打包不兼容的广告
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# 使用AdobeCreative Repackaging Service重新打包不兼容的广告{#repackage-incompatible-ads-using-adobe-creative-repackaging-service}

某些第三方广告（或创意）无法拼合到HTTP实时流(HLS)内容流中，因为其视频格式与HLS不兼容。 Primetime广告插入和TVSDK可以选择尝试将不兼容的广告重新打包到兼容的M3U8视频中。

由不同第三方提供的广告，例如代理广告服务器、库存合作伙伴或广告网络，通常以不兼容的格式投放，例如渐进式下载MP4。

当TVSDK首次遇到不兼容的广告时，播放器会忽略该广告并向创意重新打包服务(CRS)（Primetime广告插入后端的一部分）发出请求，以将广告重新打包为兼容格式。 CRS会尝试生成广告的多比特率M3U8演绎版，并将这些演绎版存储在Primetime内容交付网络(CDN)上。 下次TVSDK收到指向该广告的广告响应时，播放器将使用来自CDN的HLS兼容M3U8版本。

要启用此可选功能，请联系您的Adobe代表。

有关CRS的详细信息，请参阅 [Creative Packaging Service (CRS)](https://helpx.adobe.com/content/dam/help/en/primetime/guides/crs.pdf).

## 对CRS广告投放的多个CDN支持 {#section_900FDDA5454143718F1EB4C9732C8E1C}

虽然默认的Creative Repackaging Service (CRS)方案是使用一个Content Data Network (CDN)，但您可以在多个CDN上部署CRS资产。

由于以下原因，您可以使用多个CDN：

* 对于大型查看事件的扩展要求。
* 将CRS资产的CDN源与主内容的CDN源进行匹配的要求。

您可以使用TVSDK URL转换器API转换CRS提供的默认URL。

以下是TVSDK中的API添加内容：

* `PTURLTransformer` 一种协议，用于描述转换TVSDK请求的CRS和URL所需的方法。 应用程序可以实施此协议并提供所需方法的实现。

* `PTDefaultURLTransformer` 在TVSDK中创建并实施 `PTURLTransformer` 协议。 应用程序可以覆盖此类或添加后置URL转换处理程序。 当应用程序希望在应用默认转换后对URL请求进行更改时，此处理程序很有用。

* `PTNetworkConfiguration setURLTransformer:defaultTransformer` Setter方法提供在 `PTNetworkConfiguration` 元数据实例来设置 `PTURLTransformer` 实现。

>[!IMPORTANT]
>
>您的应用程序实施必须检查 `PTURLTransformerInputType` 枚举和仅转换URL类型 `PTURLTransformerInputTypeCRSCreative` 用于CRS。

以下代码示例显示了应用程序如何将默认主机组件更改为其他字符串(例如， `cdn.mycrsdomain.com`)：

```
// The sample code below uses Non-ARC code 
PTNetworkConfiguration *networkConfiguration = [[[PTNetworkConfiguration alloc] init] autorelease]; 
   
PTDefaultURLTransformer *defaultTransformer = [[[PTDefaultURLTransformer alloc] init] autorelease]; 
    [defaultTransformer addPostURLTransformHandler:^NSString *(NSString *url, PTURLTransformerInputType type) { 
        if (type == PTURLTransformerInputTypeCRSCreative) { 
            return [url stringByReplacingOccurrencesOfString:[NSURL URLWithString:url].host  
              withString:@"cdn.mycrsdomain.com"]; 
        } 
            return url; 
    }]; 
  
[networkConfiguration setURLTransformer:defaultTransformer]; 
   
// metadata is the PTMetadata instance set on a PTMediaPlayerItem instance. 
[metadata setMetadata:[self getNetworkConfiguration] forKey:PTNetworkConfigurationMetadataKey];
```
