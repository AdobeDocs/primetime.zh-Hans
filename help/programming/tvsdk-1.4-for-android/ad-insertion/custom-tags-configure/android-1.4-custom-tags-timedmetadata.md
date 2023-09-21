---
description: 当TVSDK检测到播放列表/清单中的订阅标记时，播放器会自动尝试处理该标记并将其以TimedMetadata对象的形式公开。
title: 定时元数据类
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---

# 定时元数据类{#timed-metadata-class}

当TVSDK检测到播放列表/清单中的订阅标记时，播放器会自动尝试处理该标记并将其以TimedMetadata对象的形式公开。

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
   <td colname="col1"> <span class="codeph"> id </span> </td> 
   <td colname="col02"> 长 </td> 
   <td colname="col2"> 定时元数据的唯一标识符。 此值通常从提示/标记ID属性中提取。 否则，将提供一个唯一的随机值。 使用 <span class="codeph"> getId </span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 元数据 </span> </td> 
   <td colname="col02"> 元数据 </td> 
   <td colname="col2"> 从播放列表/清单自定义标记中处理/提取的信息。 使用 <span class="codeph"> getMetadata </span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> name </span> </td> 
   <td colname="col02"> 字符串 </td> 
   <td colname="col2"> 定时元数据的名称。 如果类型为 <span class="codeph"> 标记 </span>，该值表示提示/标记名称。 如果类型为 <span class="codeph"> ID3 </span>，为空。 使用 <span class="codeph"> getName </span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 时间 </span> </td> 
   <td colname="col02"> 长 </td> 
   <td colname="col2"> 相对于主内容的开始时间（该定时元数据出现在流中）的时间位置（以毫秒为单位）。 使用 <span class="codeph"> getTime </span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> type </span> </td> 
   <td colname="col02"> 类型 </td> 
   <td colname="col2"> 定时元数据的类型。 使用 <span class="codeph"> getType </span>. 
    <ul id="ul_70FBFB33E9F846D8B38592560CCE9560"> 
     <li id="li_739D30561BFB4D9B97DF212E4880BA2C">TAG — 指示定时元数据是从播放列表/清单中的标记创建的。 </li> 
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
  >清单中自定义标记中的复杂数据（如带有特殊字符的字符串）必须用引号括起来。 例如：
  >
  >```
  >#EXT-CUSTOM-TAG:type=SpliceOut,ID=1,time=71819.7222,duration=30.0, 
  >url="www.example.com:8090?parameter1=xyz&parameter2=abc"
  >```
  >

* 如果提取因自定义标记格式而失败，则元数据属性将为空，并且您的应用程序必须提取实际信息。 在这种情况下，不会引发任何错误。

| 元素 | 描述 |
|---|---|
| `public enum Type { TAG, ID3}` | 定时元数据的可能类型。 |
| `public TimedMetadata(Type type, long time, long id, String name, Metadata metadata);` | 默认构造函数（time是本地流时间）。 |
| `public long getTime();` | 相对于主内容的开始位置，此元数据插入到流中的位置。 |
| `public Metadata getMetadata();` | 插入到流中的元数据。 |
| `public Type getType();` | 返回定时元数据的类型。 |
| `public long getId();` | 返回从提示/标记属性提取的ID。 否则，将提供一个唯一的随机值。 |
| `public String getName();` | 返回提示的名称，通常为HLS标记名称。 |
