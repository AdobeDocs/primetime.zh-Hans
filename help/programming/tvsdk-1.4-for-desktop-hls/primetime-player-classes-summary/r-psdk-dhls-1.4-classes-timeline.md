---
description: 这些类提供有关特定媒体的时间轴的信息，包括广告的投放。
title: 时间线类
exl-id: 8382fff2-0f10-4a8c-9c0c-66d26fe18938
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---

# 时间线类{#timeline-classes}

这些类提供有关特定媒体的时间轴的信息，包括广告的投放。

包： [com.adobe.mediacore.timeline](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/package-detail.html)

<table frame="all" colsep="1" rowsep="1" id="table_6752E908BA6546549619994A3F7D5F87"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 名称 </th> 
   <th colname="2" class="entry"> <p>描述 </p> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/ContentTracker.html" format="html" scope="external"> ContentTracker </a> </span> </td> 
   <td colname="2"> 定义如果要创建旨在与TVSDK库集成的内容跟踪模块，则必须实施的协议的接口。 <p>此界面要求您定义向远程跟踪系统报告进度事件的方式。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Opportunity.html" format="html" scope="external"> 机会 </a> </span> </td> 
   <td colname="2"> 所有机会类的基类。 机会类表示时间线上的“有趣”点。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Placement.html" format="html" scope="external"> 投放 </a> </span> </td> 
   <td colname="2"> 打包与时间轴放置相关的信息的类。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/PlacementMode.html" format="html" scope="external"> 放置模式 </a> </span> </td> 
   <td colname="2"> 投放模式的枚举，例如是插入还是替换内容。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/PlacementType.html" format="html" scope="external"> PlacementType </a> </span> </td> 
   <td colname="2"> 表示在时间轴中放置位置的放置类型的枚举；例如PRE_ROLL。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Reservation.html" format="html" scope="external"> 预订 </a> </span> </td> 
   <td colname="2"> 预订用于限制或防止对时间线上特定时间范围的进一步处理。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Timeline.html" format="html" scope="external"> 时间线 </a> </span> </td> 
   <td colname="2"> 提供用于处理时间轴标记的迭代器的界面。 表示内容的时间线，包括广告时间。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/TimelineItem.html" format="html" scope="external"> 时间线项目 </a> </span> </td> 
   <td colname="2"> 班级。 时间线项目的通用不可变表示形式。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/TimelineMarker.html" format="html" scope="external"> 时间轴标记 </a> </span> </td> 
   <td colname="2"> 表示时间轴上标记的类。 这标记了实际时间轴上的关注区域。 目前，感兴趣的区域是广告，例如，您可能希望在推移栏UI上使用不同的颜色标记这些广告。 每个标记均由位置和持续时间（以毫秒为单位）定义。 </td> 
  </tr> 
 </tbody> 
</table>
