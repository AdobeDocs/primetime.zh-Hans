---
description: 当Browser TVSDK检测到播放列表/清单中的订阅标记时，播放器会自动尝试处理该标记并将其作为TimedMetadata对象公开。
title: 定时元数据类
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---


# 定时元数据类{#timed-metadata-class}

当Browser TVSDK检测到播放列表/清单中的订阅标记时，播放器会自动尝试处理该标记并将其作为TimedMetadata对象公开。

`TimedMetadata`类提供以下元素：

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
   <td colname="col1"> <p>类型 </p> </td> 
   <td colname="col02"> <p><span class="codeph"> TimedMetadataType</span> </p> </td> 
   <td colname="col2"> <p>以下是定时元数据类型： 
     <ul id="ul_E79C375A54C64BF09A927EE8983E98E3"> 
      <li id="li_F1907521CDBE47E282A87AF0A7A1477A">TAG — 时间元数据是从播放列表/清单中的标记创建的。 </li> 
      <li id="li_5B0C0B0F247144709F86E6654A5AB500">ID3 — 定时元数据是从媒体流中的ID3标记创建的。 </li> 
     </ul> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>时间 </p> </td> 
   <td colname="col02"> <p>数字 </p> </td> 
   <td colname="col2"> <p>相对于主内容开始的本地时间位置（毫秒），其中流中存在此定时元数据。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>id </p> </td> 
   <td colname="col02"> <p>字符串 </p> </td> 
   <td colname="col2"> <p>定时元数据的唯一标识符。 </p> <p>通常从提示/标记ID属性（如果存在）中提取。 否则，它是唯一的随机值。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>name </p> </td> 
   <td colname="col02"> <p>数字 </p> </td> 
   <td colname="col2"> <p>定时元数据的名称。 </p> <p>如果类型为TAG，则值表示提示/标记名称。 如果类型为ID3，则值为null。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>内容 </p> </td> 
   <td colname="col02"> <p>字符串 </p> </td> 
   <td colname="col2"> <p>定时元数据的原始内容。 </p> <p>如果类型为TAG，则该值表示cue/tag的整个属性列表。 如果类型ID3为null。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>元数据 </p> </td> 
   <td colname="col02"> <p><span class="codeph"> 元数据</span> </p> </td> 
   <td colname="col2"> <p>从播放列表/清单自定义标签中处理/提取的信息。 </p> </td> 
  </tr> 
 </tbody> 
</table>

