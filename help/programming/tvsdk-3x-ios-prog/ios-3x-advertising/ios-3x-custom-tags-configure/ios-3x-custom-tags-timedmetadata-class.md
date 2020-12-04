---
description: 当TVSDK检测到播放列表／清单中的订阅标记时，播放器自动尝试处理该标记并以PTTimedMetadata对象的形式公开它。
seo-description: 当TVSDK检测到播放列表／清单中的订阅标记时，播放器自动尝试处理该标记并以PTTimedMetadata对象的形式公开它。
seo-title: 定时元数据类
title: 定时元数据类
uuid: d76b2a6b-2995-4559-b15d-82ded4c27eea
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%

---


# 定时元数据类{#timed-metadata-class}

当TVSDK检测到播放列表／清单中的订阅标记时，播放器自动尝试处理该标记并以PTTimedMetadata对象的形式公开它。

该类提供以下元素：

<table id="table_FFC56AC5B1E04DA99C9309C0223ABA90"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>属性</b></th> 
   <th colname="col02" class="entry"><b>类型</b> </th> 
   <th colname="col2" class="entry"><b>说明</b></th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 元数据ID</span> </td> 
   <td colname="col02"><span class="codeph"> NSString</span> </td> 
   <td colname="col2"> 定时元数据的唯一标识符。 此值通常从cue/tag ID属性中提取。 否则，提供唯一随机值。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> name</span> </td> 
   <td colname="col02"><span class="codeph"> NSString</span></td> 
   <td colname="col2"> 定时元数据的名称。 如果类型为<span class="codeph"> TAG</span>，则值表示cue/tag名称。 如果类型为<span class="codeph"> ID3</span>，则为null。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 时间</span> </td> 
   <td colname="col02"><span class="codeph"> CMTime</span></td> 
   <td colname="col2"> 相对于主内容开始的时间位置（以毫秒为单位），其中流中存在此定时元数据。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> 类型</span> </td> 
   <td colname="col02"> <span class="codeph"> PTTimedMetadataType</span></td> 
   <td colname="col2">定时元数据的类型。 
    <ul id="ul_70FBFB33E9F846D8B38592560CCE9560"> 
     <li id="li_739D30561BFB4D9B97DF212E4880BA2C">TAG —— 指示定时元数据是从播放列表／清单中的标记创建的。 </li> 
     <li id="li_E785E1DEF1CC4D9DBE7764E5D05EFAFC">ID3 —— 指示定时元数据是从媒体流中的ID3标记创建的。 </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

<!--<a id="section_737CC47997F74F80A3C5C6171ADE120E"></a>-->

请记住以下事项：

* TVSDK自动将属性列表提取为键值对，并将属性存储在元数据属性中。

   >[!TIP]
   >
   >清单中自定义标记中的复杂数据（如带有特殊字符的字符串）必须加引号。 例如：
   >
   >
   ```
   >#EXT-CUSTOM-TAG:type=SpliceOut,ID=1,time=71819.7222,duration=30.0,url=
   >"www.example.com:8090?parameter1=xyz&parameter2=abc"
   >```

* 如果提取因自定义标记格式而失败，则内容属性始终包含标记的原始数据，即冒号后的字符串。 在这种情况下不会引发错误。

| **元素** | **说明** |
|---|---|
| 标记， ID3 | 定时元数据的可能类型。 |
| `@property (nonatomic, assign) CMTime time` | 相对于主内容开始的时间位置，此元数据已插入流中。 |
| `@property (nonatomic, assign) PTTimedMetadataType type` | 返回定时元数据的类型。 |
| `@property (nonatomic, retain) NSString *metadataId` | 返回从提示／标记属性提取的ID。 否则，提供唯一随机值。 |
| `@property (nonatomic, retain) NSString *name` | 返回提示的名称，该名称通常为HLS标记名称。 |