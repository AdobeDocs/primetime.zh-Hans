---
description: TVSDK从FreeWheel和提供VAST响应的其他广告服务器获取信息。 FreeWheel在VAST响应中提供来自Moat服务的信息。 Moat服务以更准确的方式统计广告印象，以更好地显示创意人员是捕获还是忽视受众的兴趣。
seo-description: TVSDK从FreeWheel和提供VAST响应的其他广告服务器获取信息。 FreeWheel在VAST响应中提供来自Moat服务的信息。 Moat服务以更准确的方式统计广告印象，以更好地显示创意人员是捕获还是忽视受众的兴趣。
seo-title: 来自Moat的广告测量
title: 来自Moat的广告测量
uuid: 73ef3a14-7ad6-4e67-8ad3-eabbeb898a09
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---


# 来自Moat{#ad-measurements-from-moat}的广告测量

TVSDK从FreeWheel和提供VAST响应的其他广告服务器获取信息。 FreeWheel在VAST响应中提供来自Moat服务的信息。 Moat服务以更准确的方式统计广告印象，以更好地显示创意人员是捕获还是忽视受众的兴趣。

Moat是一种在从浏览器到应用程序的许多用途中测量和查看内容的服务。 Moat可跨多个平台实时生成营销分析数据。

VAST响应XML有一个属性和一个您的代码可以读取的元素、最外面的`Ad id`属性和最外面的`Extension`元素。 无论采用哪种方式，代码都可以使用TVSDK保存`Ad id`信息和`Extension`信息，然后以树结构组织信息。 通过此组织，您的代码可以从任何级别获取数据，并将其传递到任何需要的位置。 最外面的`Ad id`属性的值使代码能够协调来自关联活动的信息。

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

Freewheel还可以在`Ad`元素中设置`id`属性，如下面的示例所示。

```xml
<Ad id="118566" sequence="1">
```

请参阅类`NetworkAdInfo`的API文档。
