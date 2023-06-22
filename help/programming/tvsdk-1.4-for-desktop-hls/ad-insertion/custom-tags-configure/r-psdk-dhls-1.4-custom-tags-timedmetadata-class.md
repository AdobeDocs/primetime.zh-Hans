---
description: 当TVSDK检测到播放列表/清单中的订阅标记时，播放器会自动尝试处理该标记，并将其以TimedMetadata对象的形式公开。
title: 定时元数据类
exl-id: bf2bf78d-9063-4f54-97d9-60238b77ee93
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# 定时元数据类{#timed-metadata-class}

当TVSDK检测到播放列表/清单中的订阅标记时，播放器会自动尝试处理该标记，并将其以TimedMetadata对象的形式公开。

类提供了以下元素：

<table id="table_FFC56AC5B1E04DA99C9309C0223ABA90"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 属性 </th> 
   <th colname="col02" class="entry"> 类型 </th> 
   <th colname="col2" class="entry"> 描述 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> 内容</span> </td> 
   <td colname="col02"> 字符串 </td> 
   <td colname="col2"> 定时元数据的原始内容。 如果类型为TAG，则该值表示提示/标记的整个属性列表。 如果类型ID 3为null。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> id</span> </td> 
   <td colname="col02"> 字符串 </td> 
   <td colname="col2"> 定时元数据的唯一标识符。 此值通常提取自提示/标记ID属性。 否则，将提供一个唯一的随机值。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 元数据</span> </td> 
   <td colname="col02"> 元数据 </td> 
   <td colname="col2"> 从播放列表/清单自定义标记中处理/提取的信息。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> name</span> </td> 
   <td colname="col02"> 字符串 </td> 
   <td colname="col2">定时元数据的名称。 如果类型为 <span class="codeph"> 标记</span>，值表示提示/标记名称。 如果类型为 <span class="codeph"> ID3</span>，为空。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 时间</span> </td> 
   <td colname="col02"> 数字 </td> 
   <td colname="col2"> 相对于主内容的开始时间（该定时元数据存在于流中）的时间位置（以毫秒为单位）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> type</span> </td> 
   <td colname="col02"> 字符串 </td> 
   <td colname="col2">定时元数据的类型。 
    <ul id="ul_70FBFB33E9F846D8B38592560CCE9560"> 
     <li id="li_739D30561BFB4D9B97DF212E4880BA2C">标记 — 指示定时元数据是从播放列表/清单中的标记创建的。 </li> 
     <li id="li_E785E1DEF1CC4D9DBE7764E5D05EFAFC">ID3 — 指示定时元数据是从媒体流中的ID3标记创建的。 </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

<!--<a id="section_737CC47997F74F80A3C5C6171ADE120E"></a>-->

请记住以下内容：

* TVSDK会自动将属性列表提取到键值对中，并将属性存储在元数据属性中。

   >[!TIP]
   >
   >清单中的自定义标记中的复杂数据（例如具有特殊字符的字符串）必须用引号括起来。 例如：
   >
   >
   ```
   >#EXT-CUSTOM-TAG:type=SpliceOut,ID=1,time=71819.7222,duration=30.0,url=
   >"www.example.com:8090?parameter1=xyz&parameter2=abc"
   >```

* 如果提取由于自定义标记格式而失败，则元数据属性将为空，并且您的应用程序必须提取实际信息。 在这种情况下，不会引发任何错误。

| 元素 | 描述 |
|---|---|
| `TAG, ID3 ID3, TAG` | 定时元数据的可能类型。 |
| `public function TimedMetadata(type:String, time:Number, id:String, name:String, content:String, metadata:Metadata)` | 默认构造函数（time是本地流时间）。 |
| `content:String` | 此定时元数据的源标记的原始内容。 |
| `time:Number` | 相对于主内容开头的时间位置，此元数据插入到流中。 |
| `metadata:Metadata` | 插入到流中的元数据。 |
| `type:String` | 返回定时元数据的类型。 |
| `id:String` | 返回从提示/标记属性提取的ID。 否则，将提供一个唯一的随机值。 |
| `name:String` | 返回提示的名称，通常为HLS标记名称。 |
