---
description: TVSDK从FreeWheel和提供VAST响应的其他广告服务器获取信息。 FreeWheel在VAST响应中提供来自Moat服务的信息。 Moat服务以更准确的方式计算广告印象，从而更好地显示创意人员是捕获还是忽视受众的兴趣。
seo-description: TVSDK从FreeWheel和提供VAST响应的其他广告服务器获取信息。 FreeWheel在VAST响应中提供来自Moat服务的信息。 Moat服务以更准确的方式计算广告印象，从而更好地显示创意人员是捕获还是忽视受众的兴趣。
seo-title: 来自Moat的广告测量
title: 来自Moat的广告测量
uuid: 4de4ea5e-ef52-4b6b-b215-7601a2dfdb96
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 来自Moat的广告测量 {#ad-measurements-from-moat}

TVSDK从FreeWheel和提供VAST响应的其他广告服务器获取信息。 FreeWheel在VAST响应中提供来自Moat服务的信息。 Moat服务以更准确的方式计算广告印象，从而更好地显示创意人员是捕获还是忽视受众的兴趣。

Moat是一种服务，用于测量和查看从浏览器到应用程序的各种用途。 Moat可跨多个平台实时生成营销分析数据。

VAST响应XML有一个属性和一个您的代码可以读取的元素、最外面的 `Ad id` 属性和最外面的元 `Extension` 素。 无论采用哪种方式，您的代码都可以使用TVSDK保存信 `Ad id` 息和信 `Extension` 息，然后以树结构组织信息。 通过这个组织，您的代码可以从任何级别获取数据，并将其传递到所需的任何位置。 最外面的属性的值使 `Ad id` 您的代码能够协调来自关联营销活动的信息。

例如，FreeWheel可以返回Extensions元素中的数据。 以下是示例元素。

```xml
<?xml version="1.0"?> 
<Extensions> 
  <Extension type="FreeWheel"> 
    <Parameter name="moat"> 
      <MeasurementInfo renditionID="6398737" type="MediaFile"> 
        <MoatID><![CDATA[169843;56705;17860255;17860316;2509639;g8912342;103311138;g436558;530633]]></MoatID> 
      </MeasurementInfo> 
      <MeasurementInfo renditionID="6398739" type="MediaFile"> 
        <MoatID><![CDATA[169843;56705;17860255;17860316;2509639;g8912342;103311138;g436558;530633]]></MoatID> 
      </MeasurementInfo> 
    </Parameter> 
  </Extension> 
</Extensions> 
```

Freewheel还可以在元 `id` 素中设置 `Ad` 属性，如下面的示例所示。

```xml
<Ad id="118566" sequence="1">
```

有关API信息，请参阅类的API文档 `NetworkAdInfo`。