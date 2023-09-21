---
description: TVSDK从FreeWheel和其他提供VAST响应的广告服务器获取信息。 FreeWheel通过VAST响应提供来自Moat服务的信息。 Moat服务会准确计算广告展示次数，从而更好地显示创意人员是捕捉还是忽视了受众的兴趣。
title: 从护城河进行广告测量
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# 从护城河进行广告测量{#ad-measurements-from-moat}

TVSDK从FreeWheel和其他提供VAST响应的广告服务器获取信息。 FreeWheel通过VAST响应提供来自Moat服务的信息。 Moat服务会准确计算广告展示次数，从而更好地显示创意人员是捕捉还是忽视了受众的兴趣。

Moat是一项在多种用途（从浏览器到应用程序内）上测量广告查看情况的服务。 Moat在多个平台上实时生成营销分析数据。

VAST响应XML具有您的代码可以读取的属性和元素（最外层） `Ad id` 属性和最外层 `Extension` 元素。 无论哪种方式，您的代码都可以使用TVSDK来保存这两个 `Ad id` 信息和 `Extension` 信息，然后将信息以树形结构组织起来。 有了这个组织，您的代码可以从任何级别获取数据，并将其传递给任何需要传输到的位置。 最外部的值 `Ad id` 属性允许您的代码协调来自关联营销活动的信息。

例如，FreeWheel可以在Extensions元素中返回数据。 以下是示例元素。

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

自由轮还可以设置 `id` 中的属性 `Ad` 元素，如下面的示例所示。

```xml
<Ad id="118566" sequence="1">
```

有关API信息，请参阅该类的API文档 [网络广告信息](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/)
