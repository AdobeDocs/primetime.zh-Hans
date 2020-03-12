---
description: 当浏览器TVSDK检测到播放列表／清单中的订阅标记时，播放器会自动尝试处理该标记并将其显示为TimedMetadata对象。
seo-description: 当浏览器TVSDK检测到播放列表／清单中的订阅标记时，播放器会自动尝试处理该标记并将其显示为TimedMetadata对象。
seo-title: 定时元数据类
title: 定时元数据类
uuid: 3f276618-5f61-4b41-bd2d-78e7f32178d9
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 定时元数据类{#timed-metadata-class}

当浏览器TVSDK检测到播放列表／清单中的订阅标记时，播放器会自动尝试处理该标记并将其显示为TimedMetadata对象。

类 `TimedMetadata` 提供以下元素：

<table id="table_5827A0626EDC45F68DC3E7644F3EFF69"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 属性 </th> 
   <th colname="col02" class="entry"> 类型 </th> 
   <th colname="col2" class="entry"> 说明 </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p>type </p> </td> 
   <td colname="col02"> <p><span class="codeph"> TimedMetadataType</span> </p> </td> 
   <td colname="col2"> <p>以下是定时元数据类型： 
     <ul id="ul_E79C375A54C64BF09A927EE8983E98E3"> 
      <li id="li_F1907521CDBE47E282A87AF0A7A1477A">TAG —— 定时元数据是从播放列表／清单中的标记创建的。 </li> 
      <li id="li_5B0C0B0F247144709F86E6654A5AB500">ID3 —— 定时元数据是从媒体流中的ID3标记创建的。 </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>时间 </p> </td> 
   <td colname="col02"> <p>数字 </p> </td> 
   <td colname="col2"> <p>相对于主内容开始的本地时间位置（毫秒），其中该定时元数据存在于流中。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>id </p> </td> 
   <td colname="col02"> <p>字符串 </p> </td> 
   <td colname="col2"> <p>定时元数据的唯一标识符。 </p> <p>通常从cue/tag ID属性（如果存在）中提取。 否则，它是唯一的随机值。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>name </p> </td> 
   <td colname="col02"> <p>数字 </p> </td> 
   <td colname="col2"> <p>定时元数据的名称。 </p> <p>如果类型为TAG，则值表示提示／标记名称。 如果类型为ID3，则值为null。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>内容 </p> </td> 
   <td colname="col02"> <p>字符串 </p> </td> 
   <td colname="col2"> <p>定时元数据的原始内容。 </p> <p>如果类型为TAG，则值表示cue/tag的整个属性列表。 如果类型id ID3，则值为null。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>元数据 </p> </td> 
   <td colname="col02"> <p><span class="codeph"> 元数据</span> </p> </td> 
   <td colname="col2"> <p>从播放列表／清单自定义标签中处理／提取的信息。 </p> </td> 
  </tr> 
 </tbody> 
</table>

