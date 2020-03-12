---
description: TVSDK从FreeWheel和提供VAST响应的其他加载器获取信息。 FreeWheel在VAST响应中提供来自Moat服务的信息。 Moat服务以更准确的方式计算广告印象，从而更好地显示创意人员捕捉或忽略受众的兴趣。
seo-description: TVSDK从FreeWheel和提供VAST响应的其他加载器获取信息。 FreeWheel在VAST响应中提供来自Moat服务的信息。 Moat服务以更准确的方式计算广告印象，从而更好地显示创意人员捕捉或忽略受众的兴趣。
seo-title: 来自Moat的广告测量
title: 来自Moat的广告测量
uuid: 76fa9ca0-58bd-44fe-82ce-72fdf6fcc28c
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 来自Moat的广告测量{#ad-measurements-from-moat}

TVSDK从FreeWheel和提供VAST响应的其他加载器获取信息。 FreeWheel在VAST响应中提供来自Moat服务的信息。 Moat服务以更准确的方式计算广告印象，从而更好地显示创意人员捕捉或忽略受众的兴趣。

Moat是一种服务，用于测量和查看从浏览器到应用程序的各种用途。 Moat可跨多个平台实时生成营销分析数据。

VAST响应XML有一个属性和一个您的代码可以读取的元素，最外面的ad id属性和最外面的扩展元素。 无论采用哪种方式，您的代码都可以使用TVSDK保存广告ID信息和扩展信息，并以树结构组织信息。 通过这个组织，您的代码可以从任何级别获取数据，并将其传递到所需的任何位置。 最外面的广告id属性的值使您的代码能够协调来自关联营销活动的信息。

例如，FreeWheel可以返回Extensions元素中的数据。 以下是示例元素。

```xml
<Extensions> 
   <Extension type="FreeWheel"> 
    <Parameter name="moat"> 
     <MeasurementInfo renditionID="6398737" type="MediaFile"> 
      <MoatID> 
       <![CDATA[169843;56705;17860255;17860316;2509639;g8912342;103311138;g436558;530633]]]]> 
       <![CDATA[> 
        </MoatID> 
      </MeasurementInfo> 
      <MeasurementInfo renditionID="6398739" type="MediaFile"> 
        <MoatID> 
        <![CDATA[169843;56705;17860255;17860316;2509639;g8912342;103311138;g436558;530633]]]]> 
        <![CDATA[> 
        </MoatID> 
      </MeasurementInfo> 
    </Parameter> 
  </Extension> 
</Extensions>
```

Freewheel还可以在Ad元素中设置id属性，如下面的示例所示。

```
<Ad id="118566" sequence="1">
```

请参阅中该类的API文 `PTNetworkAdInfo` 档 `PTAdAsset`。
