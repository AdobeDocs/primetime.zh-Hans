---
title: 来自Moat的广告测量
description: 来自Moat的广告测量
copied-description: true
exl-id: 3d54ca34-0b75-4a8e-ab2d-bbe59683c2cf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# 来自Moat的广告测量 {#ad-measurement-from-moat}

TVSDK从FreeWheel和其他提供VAST响应的广告服务器中获取信息。 FreeWheel通过VAST响应提供来自Moat服务的信息。 Moat服务会准确统计广告展示次数，从而更好地显示创意人员捕获或忽视了受众的兴趣。

Moat是一项测量广告查看的服务，它可用于多种用途（从浏览器到应用程序内）。 Moat在多个平台上实时生成营销分析数据。

VAST响应XML具有一个属性和一个代码可读取的元素，即最外部的ad id属性和最外部的扩展元素。 无论哪种方式，您的代码都可以使用TVSDK来保存广告ID信息和扩展信息，并以树结构组织信息。 有了这个组织，您的代码可以从任何级别获取数据，并将其传递给任何需要去的地方。 利用最外部的广告ID属性的值，您的代码可以协调来自关联营销策划的信息。

例如，FreeWheel可以返回扩展元素中的数据。 下面是一个示例元素。

```
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

Freewheel还可以在广告元素中设置id属性，如下面的示例所示。

```
<Ad id="118566" sequence="1">
```

请参阅类AdobePSDK.NetworkAdInfo的API文档。
