---
description: 'null'
seo-description: 'null'
seo-title: 来自Moat的广告衡量
title: 来自Moat的广告衡量
uuid: a29c1e74-df15-47d2-9bd6-1d366c5cdf37
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---


# 来自Moat {#ad-measurement-from-moat}的广告测量

TVSDK从FreeWheel和提供VAST响应的其他服务器获取信息。 FreeWheel在VAST响应中提供来自Moat服务的信息。 Moat服务以更准确的方式统计广告印象，以更好地显示创意人员捕捉或忽视受众的兴趣。

Moat是一种在从浏览器到应用程序的许多用途中测量和查看内容的服务。 Moat可跨多个平台实时生成营销分析数据。

VAST响应XML有一个属性和一个您的代码可以读取的元素、最外面的广告id属性和最外面的扩展元素。 无论采用哪种方式，您的代码都可以使用TVSDK保存广告ID信息和扩展信息，并将信息组织到树结构中。 通过此组织，您的代码可以从任何级别获取数据，并将其传递到任何需要的位置。 最外面的ad id属性的值使您的代码能够协调来自关联活动的信息。

例如，FreeWheel可以返回Extensions元素中的数据。 以下是示例元素。

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

Freewheel还可以在Ad元素中设置id属性，如以下示例所示。

```
<Ad id="118566" sequence="1">
```

请参阅AdobePSDK.NetworkAdInfo类的API文档。
