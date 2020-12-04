---
description: 这些类提供有关特定媒体的时间轴的信息，包括广告投放。
seo-description: 这些类提供有关特定媒体的时间轴的信息，包括广告投放。
seo-title: 时间轴类
title: 时间轴类
uuid: 9c06fec1-d725-4fe8-9cf5-1e3ade2b7d27
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 0%

---


# 时间轴类{#timeline-classes}

这些类提供有关特定媒体的时间轴的信息，包括广告投放。

包：[com.adobe.mediacore.timeline](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/package-detail.html)

<table frame="all" colsep="1" rowsep="1" id="table_6752E908BA6546549619994A3F7D5F87"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 名称 </th> 
   <th colname="2" class="entry"> <p>说明 </p> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/ContentTracker.html" format="html" scope="external"> ContentTracker  </a> </span> </td> 
   <td colname="2"> 界面，定义要创建设计为与TVSDK库集成的内容跟踪模块时必须实现的协议。 <p>此接口要求您定义向远程跟踪系统报告进度事件的方式。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Opportunity.html" format="html" scope="external"> 机会  </a> </span> </td> 
   <td colname="2"> 所有机会类的基类。 机会类代表时间线上的“有趣”点。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Placement.html" format="html" scope="external"> 放置  </a> </span> </td> 
   <td colname="2"> 包含与时间轴放置相关信息的类。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/PlacementMode.html" format="html" scope="external"> 放置模式  </a> </span> </td> 
   <td colname="2"> 放置模式的明细列表，如插入或替换内容。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/PlacementType.html" format="html" scope="external"> 放置类型  </a> </span> </td> 
   <td colname="2"> 明细列表位置类型，指示时间轴中的位置位置；例如，PRE_ROLL。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Reservation.html" format="html" scope="external"> 保留  </a> </span> </td> 
   <td colname="2"> 预留用于限制或阻止对时间线上的特定时间范围的进一步处理。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Timeline.html" format="html" scope="external"> 时间轴  </a> </span> </td> 
   <td colname="2"> 提供用于处理时间线标记的迭代器的接口。 表示内容的时间轴，包括广告分段。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/TimelineItem.html" format="html" scope="external"> 时间轴项目  </a> </span> </td> 
   <td colname="2"> 课。 时间轴项的通用不可变表示。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/TimelineMarker.html" format="html" scope="external"> 时间轴标记  </a> </span> </td> 
   <td colname="2"> 表示时间轴上的标记的类。 这将标记实际时间线上的感兴趣区域。 目前，感兴趣的区域是您可能要标记的广告，例如，在拖拽栏UI上用不同的颜色进行标记。 每个标记由位置和持续时间（每个表示单位为毫秒）定义。 </td> 
  </tr> 
 </tbody> 
</table>

