---
description: TVSDK从FreeWheel和其他提供VAST响应的广告服务器中获取信息。 FreeWheel通过VAST响应提供来自Moat服务的信息。 Moat服务计算广告展示次数时的准确性，可以更好地表明创意人员捕捉或忽视了受众的兴趣。
title: 从护城河进行广告测量
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---

# 从护城河进行广告测量{#ad-measurements-from-moat}

TVSDK从FreeWheel和其他提供VAST响应的广告服务器中获取信息。 FreeWheel通过VAST响应提供来自Moat服务的信息。 Moat服务计算广告展示次数时的准确性，可以更好地表明创意人员捕捉或忽视了受众的兴趣。

Moat是一项在多种用途（从浏览器到应用程序内）上测量广告查看情况的服务。 Moat在多个平台上实时生成营销分析数据。

VAST响应XML具有您的代码可读取的属性和元素、最外部的ad id属性和最外部的扩展元素。 无论哪种方式，您的代码都可以使用TVSDK来保存广告ID信息和扩展信息，并以树结构组织信息。 有了这个组织，您的代码可以从任何级别获取数据，并将其传递给任何需要传输到的位置。 利用最外部的广告ID属性的值，您的代码可以协调来自关联营销活动的信息。

例如，FreeWheel可以在Extensions元素中返回数据。 以下是示例元素。

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

Freewheel还可以在广告元素中设置id属性，如下面的示例所示。

```
<Ad id="118566" sequence="1">
```

请参阅该类的API文档 `PTNetworkAdInfo` 在 `PTAdAsset`.
