---
description: TVSDK通知系统生成各种错误、警告和信息性通知，以提供诊断元数据。
title: TVSDK通知系统
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# TVSDK通知系统 {#tvsdk-notification-system}

TVSDK通知系统生成各种错误、警告和信息性通知，以提供诊断元数据。

通知对象提供与播放器状态相关的信息。 TVSDK提供了按时间顺序排序的通知对象列表，每个通知都包含以下元数据：

<table frame="all" colsep="1" rowsep="1" id="table_DBA8CACF02DB4AF2B053E560850B49CE"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 元素 </th> 
   <th colname="2" class="entry"> 描述 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> type</span> </td> 
   <td colname="2"> 通知类型。 根据平台的不同，此属性将引用可能值为INFO、WARN或ERROR的枚举类型。 这是通知的顶级分组。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 代码</span> </td> 
   <td colname="2">分配给通知的数字表示。 
    <ul id="ul_31AB497C6FFA452496DD09B0D78687B9"> 
     <li id="li_53E75022C50246E0982E315D04EFD8B3">从100000到199999的错误通知事件 </li> 
     <li id="li_11AE91D1325E4F718228E662C9C55F9A">警告通知事件，从200000到299999 </li> 
     <li id="li_6D3EA03845294DC2BAD1ACF507639E51">从300000到399999的信息通知事件 </li> 
    </ul> <p>每个顶级范围（例如错误）被划分为子范围(例如101000到101999表示播放错误)。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> name</span> </td> 
   <td colname="2">一个字符串，其中包含人类可读的代码描述，例如 <span class="codeph"> SEEK_ERROR</span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 元数据</span> </td> 
   <td colname="2">包含有关通知的其他相关信息的键/值对。 例如，名为的键 <span class="codeph"> URL</span> 与作为与通知相关的URL的值（例如导致错误的无效URL）配对。 </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> innerNotification</span> </td> 
   <td colname="2">对另一个的引用 <span class="codeph"> PTNotification</span> 直接影响此通知的对象。 一个示例可能是直接对应于时间线插入冲突的关于广告插入失败的通知。 并非所有通知都提供内部通知。 </td> 
  </tr> 
 </tbody> 
</table>
