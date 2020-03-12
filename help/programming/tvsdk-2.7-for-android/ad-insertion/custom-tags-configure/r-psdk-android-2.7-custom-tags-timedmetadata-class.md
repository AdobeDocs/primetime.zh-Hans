---
description: 当TVSDK检测到播放列表／清单中的订阅标签时，播放器会自动尝试以TimedMetadata对象的形式处理和公开该标签。
seo-description: 当TVSDK检测到播放列表／清单中的订阅标签时，播放器会自动尝试以TimedMetadata对象的形式处理和公开该标签。
seo-title: 定时元数据类
title: 定时元数据类
uuid: 45bd0d9f-3641-4041-905a-a36658c8c9ce
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 定时元数据类 {#timed-metadata-class}

当TVSDK检测到播放列表／清单中的订阅标签时，播放器会自动尝试以TimedMetadata对象的形式处理和公开该标签。

该类提供以下元素：

<table id="table_FFC56AC5B1E04DA99C9309C0223ABA90"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 属性 </th> 
   <th colname="col02" class="entry"> 类型 </th> 
   <th colname="col2" class="entry"> 说明 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> id </span> </td> 
   <td colname="col02"> 长 </td> 
   <td colname="col2"> <p>定时元数据的唯一标识符。 </p> <p>此值通常从cue/tag ID属性中提取。 否则，提供唯一随机值。 使用 <span class="codeph"> getId </span>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 元数据 </span> </td> 
   <td colname="col02"> 元数据 </td> 
   <td colname="col2"> <p>从播放列表／清单自定义标签中处理／提取的信息。 使用 <span class="codeph"> getMetadata </span>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> name </span> </td> 
   <td colname="col02"> 字符串 </td> 
   <td colname="col2"> <p>定时元数据的名称。 如果类型为 <span class="codeph"> TAG </span>，则值表示cue/tag名称。 如果类型为 <span class="codeph"> ID3 </span>，则为null。 使用 <span class="codeph"> getName </span>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 时间 </span> </td> 
   <td colname="col02"> 长 </td> 
   <td colname="col2"> <p>相对于主内容开始的时间位置（以毫秒为单位），其中此定时元数据存在于流中。 使用 <span class="codeph"> getTime </span>。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> type </span> </td> 
   <td colname="col02"> 类型 </td> 
   <td colname="col2"> <p>定时元数据的类型。 使用 <span class="codeph"> getType </span>。 
     <ul id="ul_70FBFB33E9F846D8B38592560CCE9560"> 
      <li id="li_739D30561BFB4D9B97DF212E4880BA2C">TAG —— 指示定时元数据是从播放列表／清单中的标记创建的。 </li> 
      <li id="li_E785E1DEF1CC4D9DBE7764E5D05EFAFC">ID3 —— 指示定时元数据是从媒体流中的ID3标记创建的。 </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

<!--<a id="section_737CC47997F74F80A3C5C6171ADE120E"></a>-->

请记住以下事项：

* TVSDK会自动将属性列表提取为键值对，并将属性存储在元数据属性中。

   >[!TIP]
   >
   >清单中自定义标记中的复杂数据（如带有特殊字符的字符串）必须加引号。 例如：  >
   >
   >
   ```>
   >#EXT-CUSTOM-TAG:type=SpliceOut,ID=1,time=71819.7222,duration=30.0,url= 
   >"www.example.com:8090?parameter1=xyz&parameter2=abc"
   >```  >
   >



* 如果由于自定义标记格式而提取失败，则元数据属性将为空，并且您的应用程序必须提取实际信息。 在这种情况下，不会引发错误。

<table id="table_1BAE98BF23F641A3A5709EBE37B327F6"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 元素 </th> 
   <th colname="col2" class="entry"> 说明 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public enum Type {TAG, ID3} </span> </td> 
   <td colname="col2"> <p>定时元数据的可能类型。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public TimedMetadata（类型，长时间，长id，字符串名称，元数据）; </span> </td> 
   <td colname="col2"> <p>默认构造函数（time是本地流时间）。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public long getTime(); </span> </td> 
   <td colname="col2"> <p>相对于主内容开始的时间位置，此元数据已插入流中。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 公共元数据getMetadata(); </span> </td> 
   <td colname="col2"> <p>在流中插入的元数据。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public Type getType(); </span> </td> 
   <td colname="col2"> <p>返回定时元数据的类型。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public long getId(); </span> </td> 
   <td colname="col2"> <p>返回从提示／标记属性提取的ID。 否则，提供唯一随机值。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> public String getName(); </span> </td> 
   <td colname="col2"> <p>返回提示的名称，该名称通常为HLS标记名称。 </p> </td> 
  </tr> 
 </tbody> 
</table>

