---
description: 无法将某些第三方广告（或创意）拼接到HTTP实时流(HLS)内容流中，因为其视频格式与HLS不兼容。 Primetime广告插入和TVSDK可以选择尝试将不兼容的广告重新打包到兼容的M3U8视频中。
title: 使用Adobe Creative Repackaging Service重新打包不兼容的广告
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---


# 使用Adobe Creative Repackaging Service {#repackage-incompatible-ads-using-adobe-creative-repackaging-service}重新打包不兼容的广告

无法将某些第三方广告（或创意）拼接到HTTP实时流(HLS)内容流中，因为其视频格式与HLS不兼容。 Primetime广告插入和TVSDK可以选择尝试将不兼容的广告重新打包到兼容的M3U8视频中。

来自不同第三方（如代理广告服务器、您的库存合作伙伴或广告网络）的广告通常以不兼容的格式交付，如渐进式下载的MP4。

当TVSDK第一次遇到不兼容的广告时，播放器会忽略该广告并向创意重新打包服务(CRS)发出请求，以将广告重新打包为兼容格式，该服务是Primetime广告插入后端的一部分。 CRS尝试生成广告的多位速率M3U8再现，并将这些再现存储在Primetime内容投放网络(CDN)上。 下次TVSDK收到指向该广告的广告响应时，播放器将使用CDN中与HLS兼容的M3U8版本。

要启用此可选功能，请与Adobe代表联系。

有关CRS的详细信息，请参阅[创意包装服务(CRS)](https://helpx.adobe.com/content/dam/help/en/primetime/guides/crs.pdf)。

## 对CRS广告投放{#multiple-cdn-support-for-crs-ad-delivery}的多个CDN支持

虽然默认的Creative Repackaging Service(CRS)方案是使用一个内容数据网络(CDN)，但您可以在多个CDN上部署CRS资源。

您可以出于以下原因使用多个CDN:

* 需要向上扩展以实现大型查看事件。
* 要求将CRS资源的CDN源与主内容的CDN源匹配。

您可以使用TVSDK URL Transformer API转换CRS提供的默认URL。

以下是TVSDK中新增的API:

* `URLTransformer` 描述转换TVSDK请求的CRS和URL所需方法的接口。应用程序可以实现此接口并提供所需方法的实现。

* `DefaultURLTransformer` 在TVSDK中创建并实现接口的默认URL转换器 `URLTransformer` 实例。应用程序可以覆盖此类或添加帖子URL转换处理函数。 当应用程序在应用默认转换后希望更改URL请求时，此处理函数很有用。

* `NetworkConfiguration.urlTransformer` 在元数据实例上提供的用于 `NetworkConfiguration` 设置实现的setter `URLTransformer` 方法。

>[!IMPORTANT]
>
>您的应用程序实施必须检查`URLTransformerInputType`明细列表，并且只检查CRS类型为`URLTransformerInputType.CRSCreative`的转换URL。

下面的代码示例说明应用程序如何将默认主机组件更改为其他字符串（例如`cdn.mycrsdomain.com`）：

```
var networkConfiguration:NetworkConfiguration = new NetworkConfiguration(); 
   
var urlTransformer:DefaultURLTransformer = new DefaultURLTransformer(); 
urlTransformer.addPostURLTransformHandler(function (url:String, type:String) { 
    if (type == URLTransformerInputType.CRSCreative) { 
        return url.replace(URLUtil.getServerName(url), "cdn.mycrsdomain.com"); 
    } 
    return url; 
}); 
  
networkConfiguration.urlTransformer = urlTransformer; 
   
// metadata is the Metadata instance set on a MediaResource instance. 
metadata.setMetadata(DefaultMetadataKeys.NETWORK_CONFIGURATION_KEY,  
                     networkConfiguration);
```
